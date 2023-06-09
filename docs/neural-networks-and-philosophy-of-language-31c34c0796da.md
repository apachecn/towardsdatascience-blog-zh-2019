# 神经网络和语言哲学

> 原文：<https://towardsdatascience.com/neural-networks-and-philosophy-of-language-31c34c0796da?source=collection_archive---------13----------------------->

## 为什么维特根斯坦的理论是所有现代自然语言处理的基础

![](img/1b702c1c1ed5756cb61e8e76d77d4fd4.png)

Photo by [Alexandra](https://unsplash.com/@alex_tsl?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/words?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

单词嵌入可能是人工智能历史上最美丽和浪漫的想法之一。如果语言哲学是探索语言和现实之间的关系以及我们如何能够进行有意义的对话以理解彼此的哲学分支，那么现代自然语言处理(NLP)中的这种非常具体的技术在某种意义上就是对上个世纪最相关的哲学家之一路德维希·维特斯坦根的理论的经验证明。对于维特根斯坦来说，词语的使用是社会语言*游戏中的一步棋，由相互理解的社区成员进行*。一个词的意义仅取决于它在上下文中的有用性，而不仅仅是与现有世界对象的 1:1 关系。

> 对于我们使用“意义”这个词的一大类情况，它可以这样定义:一个词的意义是它在语言中的用法。

当然，知道一个词的确切含义是一件复杂的事情，涉及许多不同的方面:它可能指代的对象，它是什么词性，它是否是一种习惯表达以及它可能带有的所有味道，等等。所有这些方面，最后都可以归结为一个:懂得利用。

*的意思是*的概念，以及为什么一组有序的字符在一种语言中具有特定的内涵，这不仅仅是哲学上的兴趣，而是可能是从事 NLP 工作的人工智能专家每天都必须面对的最大挑战。作为说英语的人，理解“狗”是一种“动物”,并且更像“猫”而不是“海豚”,这是非常琐碎的，但是这个任务远不容易以系统的方式来解决。稍微调整一下维特根斯坦的理论，我们可以说狗和猫很相似，因为它们经常出现在相同的上下文中:更有可能找到与“房子”和“花园”等词相关的狗和猫，而不是与“大海”和“海洋”等词相关的狗和猫。这种直觉是 **Word2Vec** 的核心，这是最著名和最成功的单词嵌入实现之一。如果今天的机器距离真正理解长文本和段落还很遥远，那么毫无疑问，单词嵌入是过去十年中允许该领域朝着这个方向迈出最大一步的唯一技术。

## 从 BoW 到 Word2Vec

许多计算机科学相关任务中的一个初始问题是用数字形式表示数据；单词和句子可能是以这种方式表示的最具挑战性的数据类型。在我们的设置中，从由 **D** 个不同单词组成的词汇表中选择单词，集合中的每个单词都可以关联到一个数字索引 **i** 。几十年来使用的经典方法是将每个单词表示为一个 D 大小的数字向量，由除了位置 I 处的 1 之外的所有 0 组成。以仅由 3 个单词组成的词汇为例:“dog”、“cat”和“dolphin”(D = 3)。每个单词可以表示为一个 3 维向量:“狗”对应于[1，0，0]，“猫”对应于[0，1，0]，“海豚”，显然对应于[0，0，1]。作为一个简单的扩展，文档可以表示为一个 D 大小的向量，其中每个元素计算文档中第 I 个单词的出现次数。这种方法被称为单词袋(BoW ),已经使用了几十年。

虽然 BoW 在 90 年代取得了成功，但它缺少一个非常酷的词汇特征:意义。我们*知道*两个非常不同的单词可能有相似的意思，即使从正字法的角度来看它们完全不同。“猫”和“狗”都代表宠物，*“国王”和“王后”的意思完全一样，只是体裁不同，“苹果”和“香烟”完全没有关系。我们*知道*这一点，但是使用弓模型，它们在向量空间中的距离都是一样的，1。同样的问题也可以扩展到文档:使用 BoW，我们可以说，只有当两个文档在一定次数上包含完全相同的单词时，它们才是相似的。这就是 Word2Vec 的用武之地，它将维特根斯坦 60 年前在他的*哲学研究*中所做的大量哲学讨论用机器学习的术语表达出来。*

*给定大小为 D 的字典，其中单词由其索引标识，目标是学习每个单词的 N 大小的向量表示，其中 N <<d. ideally="" we="" want="" this="" n-sized="" vector="" to="" be="" dense="" and="" able="" represent="" some="" semantic-specific="" aspects="" of="" meaning.="" for="" example="" that="" class="ls">、狗和猫具有相似的表示，而“苹果”和“香烟”*、*在向量空间中具有非常远的表示。我们希望能够对像 king+woman-man = queen 这样的向量进行一些基本的代数运算，或者说代表“男演员”和“女演员”的向量之间的距离和“王子”和“公主”之间的距离差不多。尽管这些结果非常理想化，但实验表明通过 Word2Vec 获得的载体表现出与这些非常接近的性质。</d.>*

*Word2Vec 不直接学习这些表示，而是作为无监督分类任务的副产品获得它们。一个平均的 NLP 数据集(称为语料库)由一组句子组成；属于一个句子的每个单词都出现在周围单词的上下文中。分类器的目标是在给定其上下文单词作为输入的情况下预测目标单词。提取像“一只棕色的狗在花园里”这样的句子，单词[a，brown，is，in，the，garden]被提供作为模型的输入，输出单词“dog”是要预测的单词。这项任务被认为是无监督的学习，因为语料库不需要使用外部真实来源进行标记:给定一组句子，总是可以自动创建正面和负面的例子。将“一只棕色的狗在花园里”视为正面示例，我们可以创建大量负面样本，如“一架棕色的飞机在花园里”或“一只棕色的东西在花园里”，用从数据集中提取的随机单词替换目标单词“狗”。*

*现在维特根斯坦的理论的切入点已经很清楚了:语境对于学习嵌入是至关重要的，正如在他的理论中赋予意义是至关重要的一样。正如两个单词具有相似的意思一样，它们将具有相似的表示(N 维空间中的小距离),因为它们经常出现在相似的上下文中。所以“猫”和“狗”将最终具有相近的向量，因为它们经常出现在相同的上下文中:模型对它们使用相似的嵌入是有用的，因为这是在给定上下文的情况下预测两个单词时具有更好性能的最方便的事情。*

*原始论文提出了两种不同的体系结构:CBOW 和 Skip-gram。在这两种情况下，单词表示与特定于味道的分类任务一起被训练，提供最佳可能的向量嵌入，最大化模型的性能。*

*![](img/dd28d9ad5bbfb727118d0b6624e0e057.png)*

*Figure 1 — Architecture comparison between CBOW and Skip-gram*

***CBOW** 代表连续单词包，其目标是在给定输入上下文的情况下正确预测单词。输入和输出被提供为 D 大小的向量，并被投影到共享权重的 N 大小的空间中。用于将 D 大小的向量投影到 N 大小的内部向量的权重是我们正在寻找的嵌入。基本上，单词嵌入被表示为一个 D×N 矩阵，其中每行代表词汇表中的一个单词。所有上下文单词被投影到相同的位置，并且它们的向量表示被平均化；因此，单词的顺序不影响投影。*

***Skip-gram** 做了同样的事情，但是又恢复了:试图预测作为目标词输入的 **C** 上下文词。预测多个上下文单词的问题可以被重塑为一组独立的二元分类任务，现在的目标是预测上下文单词的存在(或不存在)。*

*根据经验，Skip-gram 需要更多的时间来训练，并且通常会给出稍微好一点的结果，但是，像往常一样，不同的应用程序有不同的要求，并且很难预先预测两者中哪一个会优于另一个。由于优化模型权重所需的数据量和计算能力，这个概念看起来很简单，训练这种架构是一场噩梦。幸运的是，一些预先训练好的单词嵌入可以在网上找到，并且只需几行代码就可以探索向量空间——最有趣的部分。*

## *可能的改进:手套和快速文本*

*在经典的 Word2Vec 之上，并遵循或多或少相同的方法，在过去几年中已经提出了大量可能的改进。最有趣和最常用的两个是 GloVe(由斯坦福大学开发)和 fastText(由脸书开发),主要是因为它们强调并试图克服原始算法的局限性。*

*在[原始 GloVe 论文](https://nlp.stanford.edu/pubs/glove.pdf)中，作者强调了在单独的本地上下文中训练模型如何很好地利用了语料库的全局统计数据。克服这个限制的第一步是创建一个全局矩阵 **X** ，其中每个元素 I，j 计算单词 **j** 在单词 **i** 的上下文中出现的次数。本文的第二个最大贡献是理解了这些原始概率本身在确定意义方面并不强大，引入了一个共现矩阵，从这个矩阵中可以直接提取意义的某些方面。*

> *考虑两个单词 I 和 j，它们展示了感兴趣的特定方面；具体来说，假设我们对热力学相的概念感兴趣，我们可以取 i =冰，j =蒸汽。可以通过研究这些词与各种探测词 k 的共现概率的比率来检查这些词的关系。对于与冰而不是蒸汽相关的词 k，假设 k =固体，我们预计比率 Pik/Pjk 将很大。同样，对于与蒸汽有关但与冰无关的单词 k，比如说 k =气体，比例应该很小。对于像水或时尚这样的词，要么与冰和蒸汽都有关系，要么两者都没有关系，比率应该接近 1。*

*这个概率比现在是学习嵌入的起点。我们希望能够计算出与特定函数结合的表示，F 在嵌入空间中保持这个比例常数。*

*![](img/45dedf0b7bbfc405e4024d83d8d8a805.png)*

*Figure 2 — Most general formula for GloVe embeddings*

*函数 F 和单词 k 的相关性可以被简化，并由指数和固定偏差代替，作为结果给出这个最小平方误差函数 **J** :*

*![](img/2a2c5bc5d1290ee3ef6baac8da6c559f.png)*

*Figure 3 — Final scoring function for computing GloVe embeddings*

*函数 **f** 是一个评分函数，它试图不对太频繁和太罕见的共现进行加权，而 **bi** 和 **bj** 是用于恢复函数对称性的偏差。在论文的最后几段中，展示了如何训练该模型，最终与训练经典的跳格模型没有太大的不同，即使经验测试显示 GloVe 如何优于 Word2Vec 实现。*

*另一方面，fastText 对 Word2Vec 提出了完全不同的批评:从 D 大小的 one-hot 编码向量开始训练模型的缺点是忽略了单词的内部结构。fastText 提出学习字符 n-gram 的表示，并将单词表示为 n-gram 向量的总和，而不是一次性编码单词来学习单词表示。例如，在 n=3 的情况下，单词“flower”被编码为 6 个不同的 3-gram[<fl、flo、low、owe、wer、er > ]加上特殊序列< flower >。注意尖括号是如何用来表示单词的开始和结束的。因此，一个单词由其在单词字典中的索引及其包含的 n 元语法集来表示，并使用哈希函数映射到整数。这个简单的改进允许跨单词共享 n 元语法表示，并计算没有出现在训练语料库中的单词的嵌入。*

## *实验和可能的应用*

*正如所承诺的，**使用**这些嵌入只是几行 Python 代码的问题。我用一个 50 码大小的手套模型和一个 300 码大小的 fastText 模型进行了一些实验，前者训练了 60 亿个单词，这些单词是从主要在维基百科上检索的句子中提取的，后者训练了 6000 亿个令牌。在这一段中，来自两者的结果混合在一起，只是为了证明概念并给出对主题的一般理解。*

*首先，我想测试一些基本的单词相似性，这是单词嵌入的最简单也是最重要的特性。不出所料，与“狗”这个词最相似的词是“猫”(0.92)、“狗”(0.85)、“马”(0.79)、“小狗”(0.78)、“宠物”(0.77)。请注意，复数形式与单数形式的意思非常相似。再说一次，对我们来说这么说是很琐碎的，但对机器来说，这是完全不同的事实。现在的食物:和“披萨”最相似的词是“三明治”(0.87)、“三明治”(0.86)、“零食”(0.81)、“面包店”(0.79)、“薯条”(0.79)、“汉堡”(0.78)。有道理，结果令人满意，模型表现相当好。*

*下一步是尝试在向量空间中执行一些基本代数，以检查我们的模型是否正确地学习了一些期望的行为。“女演员”(0.94)这个词可以作为女人+演员-男人的结果得到，“国王”(0.86)作为男人+女王-女人。一般来说，如果在意义上 a : b = c : d，单词 **d** 应该是 d = b-a+c。更进一步说，这种向量运算甚至能够描述地理方面，这令人难以置信:我们知道罗马是意大利的首都，因为柏林是德国的首都，事实上柏林+意大利-罗马=德国(0.88)和伦敦+德国-英格兰=柏林(0.83)。*

*现在最有趣的部分，按照同样的想法，我们可以尝试加减概念，看看会发生什么。例如，意大利人的比萨饼在美国相当于什么？披萨+美国-意大利=汉堡(0.60)，其次是芝士汉堡(0.59)。自从我搬到荷兰，我总是说这个国家是三种东西的混合体:一点点美国资本主义、瑞典人的冷漠和生活质量，以及最后一点点那不勒斯*的繁荣。*稍微调整一下原始定理，去掉一点瑞士精度，我们得到荷兰(0.68)为美国+瑞典+那不勒斯-瑞士:老实说，相当令人印象深刻。*

*![](img/a8c49be13f7469043e298b19d433aa6e.png)*

*Figure 4 — To all the Dutch readers: take this as a compliment. Ok?*

*可以在[这里](http://mccormickml.com/2016/04/12/googles-pretrained-word2vec-model-in-python/)和[这里](http://kavita-ganesan.com/gensim-word2vec-tutorial-starter-code/)找到使用这种预训练嵌入的良好动手起点。Gensim 是一个用 Python 编写的简单而完整的库，有一些现成的代数和相似函数。这些预先训练的嵌入可以以许多不同的(和有用的)方式使用，例如，提高情感分析器或语言模型的性能。而不是喂养这些模型(不管他们的任务是什么！)对于一个热编码字，使用这些 N 大小的向量将显著提高性能。当然，训练特定领域的嵌入可以带来更好的性能，但是训练这种架构所需的时间和精力可能有点多余。*