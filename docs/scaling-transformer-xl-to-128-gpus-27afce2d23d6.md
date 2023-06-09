# 将 Transformer-XL 扩展至 128 个 GPU

> 原文：<https://towardsdatascience.com/scaling-transformer-xl-to-128-gpus-27afce2d23d6?source=collection_archive---------15----------------------->

[本·曼](https://medium.com/u/33ebef5d1079?source=post_page-----27afce2d23d6--------------------------------)，[雅罗斯拉夫·布拉托夫](https://medium.com/u/5511064b4364?source=post_page-----27afce2d23d6--------------------------------)，大流士·拉姆

**TL；DR:** 我们在 AWS 上的 128 个 GPU 上高效地进行了 Transformer-XL 训练。该代码可在[https://github.com/cybertronai/transformer-xl](https://github.com/cybertronai/transformer-xl)获得

![](img/21a9ff2a44ee520cffeb28e32f8f6a34.png)

We achieved almost linear throughput scaling on AWS p3dn.24xlarge instances with 8 V100–32GB each on a 100Gbps network

# 概观

研究语言模型的困难之一是，你通常不知道你的想法是否可行，直到你在真实世界的数据集上尝试它们。然而，在一台机器上对这样的数据集进行训练可能需要数周时间。

幸运的是，有一个简单的方法可以加速这个过程:

1.  找一个好的单机型号
2.  在 N 台机器上并行运行模型的 N 个副本，每一步都要同步
3.  解决所有剩余的技术挑战

我们使用这个方法将 ImageNet 培训时间从 2 周减少到 [18 分钟](https://github.com/diux-dev/imagenet18)。您还可以应用相同的优化在 2 周内训练一个模型，这原本需要 4 年，因此您可以选择扩大您的研究范围，而不是迭代时间。

通过几分钟的训练，图像模型训练“基本上解决了”，而语言模型训练时间仍然是创新的障碍。我们的目标是看看通过在云中分布我们的培训，我们可以增加多少培训吞吐量。

对于单机模型，我们选定了 Transformer-XL 的[正式实现](https://github.com/kimiyoung/transformer-xl/)。这种体系结构在语言建模方面取得了几项最先进的成果。作者通过发布代码和指令，使得重现他们的结果变得很容易。

一旦我们在他们的[自述文件](https://github.com/kimiyoung/transformer-xl/tree/master/pytorch#replicate-the-ppl--2403-result-on-wikitext-103-with-transformer-xl)中重现了准确性，我们就迭代性能，在不影响质量的情况下获得大约 2.6 倍的吞吐量提升。

然后，我们将这个模型扩展到在多台机器上训练，使用 all-reduce 来同步梯度。分布式语言模型每一步发送的数据至少比典型的图像模型多 10 倍，因此我们使用 AWS p3dn 实例来实现 100 Gbps 的网络连接。这些实例有 32GB 的 GPU 内存，因此我们能够通过增加每个 GPU 的批处理大小来将培训效率再提高 25%。最终结果是:一个 64 GPU 版本的 small Transformer-XL 模型的训练速度比原来“慢”的 4 GPU 实现快 44 倍。我们的 Transformer-XL 具有 75M 参数(相当于论文中的 186M)，在 128 GPUss 上的训练速度比在 8 GPU 上快 13.2 倍。

训练程序需要改变，以防止更大批量的数值发散，所以我们遵循谷歌在他们的 1024 TPU 缩放[论文](https://arxiv.org/abs/1904.00962)中提供的配方。我们在一个独立的[回购](https://github.com/cybertronai/pytorch-lamb)中开源了这个优化器。

# 技术细节

## 资料组

我们主要用 [Wikitext-103](https://blog.einstein.ai/the-wikitext-long-term-dependency-language-modeling-dataset/) 进行实验，这是一个由维基百科的预标记子集组成的标准语言建模数据集。训练集在 515MB 中包含大约 1 亿个标记和 267K 个唯一单词。它使用了修改过的[摩西记号化](https://github.com/alvations/sacremoses)，用< UNK >符号替换 0.4%的单词来限制 vocab 的大小。Transformer-XL 代码库在训练开始时将整个数据集加载到 GPU 内存中。

为了在训练时加快速度，我们对数据集进行了预编码，并将它们放入 AWS 磁盘映像中。

## 基础设施

我们已经自动化了许多常见的任务，这些任务来自于分布式培训系统的原型设计，并将它们打包成一个工具 [ncluster](https://github.com/yaroslavvb/ncluster) 。其理念是任何频繁的任务都应该是单一的命令行调用。一些例子:

1.  提出一些实例，以现货价格进行测试
2.  修复一个错误，并在 30 秒内重新启动多机实验。
3.  登录到最近的机器，看看它在做什么
4.  保持远程计算机上的文件夹与本地文件夹同步
5.  登录到另一个用户的计算机来解决问题

## 以太网

我们尝试了各种网络配置来寻找可以优化吞吐量的设置。运行 iperf3 [测试](https://github.com/cybertronai/bflm/blob/master/infra/launch_network_test.py)，我们可以看到机器之间的吞吐量为 93 Gbps，而 NCCL all-reduce 性能下降到大约 50 Gbps 的[。AWS 网络设置的一个特点是每个网络流量被限制在大约 10 Gbps，因此我们使用多个 NCCL 环来支持多个流量。由于 NCCL 最新版本中的一个](https://github.com/cybertronai/bflm/blob/master/infra/pytorch_bandwidth_benchmark_numbers.txt)[错误](https://github.com/NVIDIA/nccl/issues/209)，我们不得不恢复到旧版本，旧版本支持多个流，但是没有有效地利用带宽。特别是，随着我们增加 GPU 的数量，传输的字节量增加了 4 倍，这是像 ring-allreduce 这样的带宽恒定算法所没有预料到的。然而，当我们让 LAMB 工作并且我们的本地批处理大小达到 32GB RAM 的饱和时，我们的网络需求下降得足够多，即使每台机器的通信负载过大，我们也没有达到带宽限制。

在某个时候，我们注意到我们最高效的带宽运行表现不佳，性能下降了 30%(见左下图)。一些调查显示，过于接近内存限制会导致 CUDA 缓存分配器反复耗尽内存，并在垃圾收集期间导致额外的同步(下图)。解决方案是通过降低批处理大小来稍微减少内存使用，这样问题就消失了。

![](img/0499abc6578e92e4f870586e7efcf55a.png)

Left: backwards time in ms, right: torch.cuda.memory_cached()

我们发现运行之间存在一些吞吐量差异。例如，一个不幸运的 64 GPU 运行将需要 2.5 分钟来完成 wt103 的一个纪元，而一个“幸运的”128 GPU 运行可以在 1 分钟内完成。我们认为这是由于 AWS 集群放置组是近似的:AWS 试图将放置组中的所有实例放置到本地连接的配置或“砖”上，但当这不可能时，一些实例将溢出到相邻的砖。

## 混合精度

依靠 16 位精度，我们可以利用 Volta TensorCores 减少内存使用，提高处理速度。我们测试了两种形式的 fp16 训练——纯 fp16 和混合精度训练。在纯 fp16 模式下，所有操作的精度都会降低。我们无法匹配纯 fp16 中的准确性数字，因为训练会很快变得不稳定。

在混合精度训练中，我们在 fp32 中保留一个权重的主副本，并在每个优化器步骤中对该主副本进行更新，然后将权重转换为 fp16，以便向前传递。这使我们能够在节省空间的同时保持精度。动态损耗缩放增加了传播的梯度信息量，同时保持了数值稳定性。为了实现这些，我们使用了 NVidia 开发的 Apex 和威震天包中的代码。

在合成实验中，我们发现张量核没有被完全激活，除非维度是 8 的倍数。

![](img/62f5b425a28e181d2001717b79f4aad4.png)

Figure 1: Time to multiply *n* x *n* matrices. Orange is fp32, blue is fp16\. The Y axis shows log seconds averaged over three runs.

使用 tensorcores，fp16 矩阵乘法对于大的 *n* 几乎快 10 倍。注意，对于小的 *n* ，使用半精度带来的性能提升可以忽略不计。

![](img/a38ec9e210fa44921e6e61182bc14c04.png)

Figure 2: However, when *n* is shifted by one, so that *n* is not a multiple of 8, fp16 performs equally with fp32, ie there is no performance increase at all and we simply save memory.

通过修改模型大小，我们能够显著提高速度，从最初的 1.2 倍提高到 2 倍，方法是转换为混合精度并增加批量大小。

## 小绵羊

LAMB optimizer 使用了[这是一个简单的调整](https://medium.com/p/46f8c0ae4866),据说它允许学习率随着工人的全局批量大小而线性增长。LAMB 将每个参数的学习率乘以权重(r1)的范数与 Adam 步骤(r2)的范数之比(r)。

如何解释下面的左图:Y 轴显示处理的令牌数的时间步长，第一个在顶部。X 轴是直方图桶，例如 N 个样本的值在 0 和 1、1 和 2 之间，等等。Z 轴是网络中每个参数值的直方图频率，例如 X%的图层权重落在 0 到 1 的范围内。你可以把它想象成每个时间步长的一个直方图，按时间堆叠，这样我们就可以看到直方图是如何随时间变化的。右图显示了相同的数据，但显示为面积图。颜色越深意味着越多的直方图柱在阴影区域中具有值，X 轴是时间，Y 轴是值(例如 r1 的权重的范数)。

![](img/99adf6476ce95c43b7192dc03bc0c758.png)

大多数参数权重(r1)始终接近 0，但一些会增长和扩散，一些会变得相当大(最大 6.5 桶)

![](img/aee174229ea85792381c3e5ed8ebfefe.png)

亚当步长规范(r2)在开始时非常大，但很快稳定在 0 到 0.5 之间。

![](img/370b1d354ae49c54333208deab50baf0.png)

上述两个影响导致信任比(r)促使一些参数长时间持续增长，在剪辑值为 10 时达到最大值。

在我们的测试中，我们发现 LAMB 甚至在一台全局批量为 768 的 p3dn . 24x 大型机器上也产生了影响，而 Adam 立即出现了分歧。我们还发现，我们可以完全消除学习速率计划中的预热，因为在训练开始时，梯度很大，这导致 LAMB 信任比很小，并降低了最不稳定层的学习速率。

也就是说，我们没有看到兰姆论文描述的线性缩放。他们没有公布他们的代码，甚至没有公布他们的超参数的细节，所以需要什么来使这个工作仍然有待观察。

## 字节对编码与自适应嵌入

Wikitext-103 的 vocab 大小为 267K，这需要很大的模型空间来表示。我们尝试切换到字节对编码(BPE)，这在机器翻译中已经显示出了性能优势。我们使用 [OpenAI 的 BPT](https://github.com/huggingface/pytorch-pretrained-BERT/blob/master/pytorch_pretrained_bert/tokenization_gpt2.py) 实现，因为它可以处理超出词汇表的序列。

Transformer-XL 有一个非常大的 vocab 大小(267K)，所以大多数参数都在令牌嵌入中。我们能够使用 vocab 大小为 50K 的 BPE 来减少模型大小，这将我们的小模型配置从 186M 减少到 75M 参数，同时具有相同的表示能力。最初的 Transformer-XL 代码使用[自适应输入和 softmax](https://openreview.net/pdf?id=ByxZX20qFQ) 来减少嵌入大小。

一个稍微棘手的细节是，BPE 产生的标记比 Wikitext-103 长 15%。这是意料之中的，因为 Wikitext-103 已经被标记化了(比如把“不”分成“不”。如果不是这样，BPE 可能会把“不”作为一个单独的标记来处理，而 Wikitext-103 的标记器会把它分开。在 BPE，通过将字符分割成单独的字节，将词汇表以外的单词分解成词汇表中的子单词片段，即使是 unicode 也是如此。这种行为是标记化长度增加 15%的原因。

在我们的消融研究中，我们发现，在考虑标记化长度后，以每个标记的训练损失衡量的性能几乎相同。由于模型规模更小，每秒令牌数增加了约 10%,而对于相同的批处理规模，GPU 利用率显著下降，从约 90%降至约 55%。这意味着当我们扩展到更大的模型时，我们可以保持每个 GPU 更高的批处理大小。

为了公平起见，我们还在大型模型配置上将 BPE 与自适应嵌入进行了比较:

![](img/4e2580ccc653cc2d1f5f2e5b30c8f3f3.png)

为了验证困惑进行转换是 math . exp(math . log(26.25)* 1950/1699)= 42.5，所以令人印象深刻的等价(尽管上面看起来不一样)！尽管我们使用的 BPE 编码是在网络的一般样本(OpenAI 的网络文本数据集)上训练的，而不是在我们的训练集 Wikitext-103 上训练的。

这两种技术是兼容的，所以将它们结合起来可能会很有趣。也就是说，由于 BPE 如此灵活，代码也更简单，我们倾向于在未来的实验中只使用它。

## 学习率探测器

在 [fast.ai part 2](http://course18.fast.ai/part2.html) 中了解到这个想法后，Ben 很兴奋地看到它的工作。亚当的情况很好:

![](img/3bf4d560f678d271aad2d225b327fe86.png)

上图的最小值恰好就是文中用到的学习率(0.00025)！我们只需要运行几分钟就可以发现这一点，这比传统的完整超参数搜索要便宜得多，在传统的完整超参数搜索中，您将使用您打算稍后使用的单个 LR 时间表运行至少一个时期。

当应用于兰姆时，发现者明显高估了学习率。

![](img/40aa1817d630d4d473b23703d5e2f712.png)

灰色曲线最小损失处的学习率为 0.0263；橙色(使用重量衰减 1e-4)为 0.0435。但是当我们以 0.01 的学习率运行它时，它仍然发散。我们不得不一直降到 0.005，以获得稳定的收敛。我们认为这是因为 LAMB 导致实际的每层学习率在训练的不同时间差异很大，导致学习率查找器不在分布范围内。我们或许可以通过运行学习率查找器更长时间来解决这个问题，或者在训练中的一个检查点上。相反，我们选择做一个更传统的学习率超参数搜索。

## 批量缩放

在我们的许多实验中，我们发现当我们通过使用更多的 GPU 来增加全局批量时，收敛速度在短期内会下降。为了试验这种效果，我们尝试在单台机器上调度批量大小。我们发现，尽管这在短期内有所帮助，但随着我们训练时间的延长，这种好处消失了。

![](img/2747a76b4315604ec7f093149dcc8611.png)

对初始收敛速度增加的一个解释是，我们在不同的批量中使用了恒定的学习速率，这导致了每个例子的学习速率更高。最后蓝色和灰色线之间的差距约为 1 亿个令牌(1 小时)，因此它确实有大约 10%的帮助，即使我们没有使用整个 GPU 容量。

![](img/8541464725a9dcc073c3b2894fcde73b.png)

然而，如果我们保持基本学习速率不变，并应用线性学习速率缩放来调整不同批量的学习速率，则训练会发散。

![](img/fa377be1d6afb3665678e4361f53d311.png)

对这些影响的更原则性的解释可能来自于[梯度噪声标度](https://arxiv.org/abs/1812.06162)。可以通过将工人批次中的梯度范数与全局批次中的梯度进行比较来估计噪声等级。在训练开始时或对于小数据集，噪声尺度较小，因此高温(η/B)训练更快。随着损耗的减少，我们需要降低温度来继续训练。

## 所有的维基百科

下图显示了 Wikitext-103 上大模型配置的训练损失与验证损失。你可以在下面的图表中看到，在仅仅 8 亿个令牌(1.5 小时)中，我们的验证损失停止下降，这表明我们过度拟合了数据集。

![](img/8f98735030cba5b71914d17bbb6eed72.png)

出于这个原因，我们很高兴尝试在 NVIDIA 的所有维基百科转储上进行培训，这比 Wikitext-103 大 25 倍。

*   它是 12GB 的文本，所以我们不能将它全部加载到 GPU 内存中
*   它被存储为 JSON，所以首先需要在保持文章边界的情况下将其扁平化
*   它包含任意的唯一标记，所以需要一些技巧来限制 vocab 的大小

幸运的是，Transformer-XL 已经包含了一个用于 10 亿单词语料库的多文件数据加载器，所以只需要一点点按摩就可以让它工作了。请注意，因为标记化不同，所以不应比较损失数字。下面，我们展示了使用 64 个 GPU 在所有维基百科上以每小时约 6 亿个令牌的速度运行两次。我们发现验证损失对学习速率非常敏感。

![](img/953837e0d83b0307e046cddbdf209d21.png)

在进一步的实验中，我们发现在不降低学习率的情况下，损失并没有减少。我们将继续试验学习率计划以提高性能。我很想尝试的一种方法是[波动-耗散关系](https://arxiv.org/abs/1810.00004)，它试图动态降低学习率。

# 结论

我们已经展示了如何在 Transformer-XL 的小型配置上，通过使用

*   AWS 100Gbps 网络
*   Pytorch 的分布式数据并行+ NCCL
*   BPE
*   小绵羊
*   混合精度

我们进行了数百次实验来提高收敛速度。到目前为止，我们还没有在标准基准测试中击败最先进的技术。也就是说，我们的高通量使我们能够以同样的成本更快地进行实验。我们还在用 spot 实例进行实验，这对于运行一个小时或更短时间的实验开始变得可行。

你是在做 AWS 的语言建模研究吗？试试[我们的代码库](https://github.com/cybertronai/transformer-xl)，让我们知道你的想法！

## 承认

这项工作是以下各方共同努力的结果

Ben —数据管道、LAMB、参数搜索和调整
Darius —使用混合精确训练在单机模型上实现 2 倍加速
Yaroslav —实验基础设施、分布式训练

另外感谢 AWS 提供计算资源。