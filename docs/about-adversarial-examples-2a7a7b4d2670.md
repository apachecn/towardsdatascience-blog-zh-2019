# 关于对立的例子

> 原文：<https://towardsdatascience.com/about-adversarial-examples-2a7a7b4d2670?source=collection_archive---------19----------------------->

## 关于什么、为什么和如何使用对立例子的概述

![](img/c3ecaceaec5cf41acbf8f7857ee989e4.png)

在深度神经网络的世界中，对立的例子是一个有趣的话题。这篇文章将试图解决这个话题的一些基本问题，包括如何产生这样的例子，并对它们进行防御。以下是我们将要介绍的内容:

1.  什么是对立的例子？
2.  为什么重要？
3.  为什么会发生？
4.  如何生成对抗性的例子？
5.  我们如何防御对立的例子？

## **1。什么是对立的例子？**

一般来说，这些输入旨在使模型错误地预测。在计算机视觉环境中思考这一现象更容易理解——在计算机视觉中，这些是输入图像的小扰动，会导致模型的错误分类。

![](img/1d3954d10a034189f3ac9281ccf77348.png)

**From** [**Explaining and Harnessing Adversarial Examples**](https://arxiv.org/abs/1412.6572) **by Goodfellow et al.**

虽然这是一个有针对性的对立示例，其中图像的变化是人眼无法检测到的，但非针对性示例是那些我们不太关心对立示例对人眼是否有意义的示例——它可能只是人眼的随机噪声。

![](img/1c8cba640146dbfcf72921646e65b583.png)

**A non-targeted “3” from** [**Tricking Neural Networks: Create your own Adversarial Examples**](https://ml.berkeley.edu/blog/2018/01/10/adversarial-examples/) **by Daniel Geng and Rishi Veerapaneni**

我不能完全准确地说，有针对性的对抗性例子是图像的变化是人眼无法察觉的。虽然扰动很小， [***有证据表明，在一个有时间限制的环境中，即使是人类也会被对抗性的例子***](https://arxiv.org/pdf/1802.08195.pdf) 所愚弄。

## 2.为什么重要？

在开始解释为什么这个话题很重要之前，让我们先弄清楚几个定义。根据攻击者的知识水平，对抗性攻击可以分为白盒攻击或黑盒攻击。白盒攻击是指对手完全了解被攻击的模型，如权重、偏差、使用的超参数等。黑盒攻击的对手是只知道模型输出的普通用户。

对抗性攻击是一个重要的研究和考虑的主题，因为它已经表明，对抗性的例子从一个模型转移到另一个模型。换句话说，为欺骗一个模型而生成的对立例子也可以欺骗使用不同架构的其他模型，或者使用相同任务的不同数据集进行训练。现在，这变成了一个巨大的安全风险，因为攻击者可以为与目标模型相同的任务开发本地模型，为本地模型生成对立的示例(就本地模型而言是白盒)，并使用它们来攻击目标(可转移性使得对目标模型的黑盒攻击更容易)。这使得大量主流或即将成为主流的应用面临风险，如面部识别、自动驾驶汽车、生物识别等，这些应用利用了基于 ML 的计算机视觉模型。

[***本文***](https://arxiv.org/pdf/1607.02533.pdf) 探讨了这在现实世界中的威胁有多大，因为在现实世界的许多使用案例中，输入来自摄像头和其他传感器。它证明了即使通过摄像机输入对立的例子也会导致错误分类。 [***这是另一篇论文***](https://arxiv.org/pdf/1707.07397.pdf) 通过生成在变换分布上保持稳健的示例，并使用 3D 打印来创建稳健的 3D 敌对对象，来展示现实世界的威胁。

## 3.为什么会发生？

深度学习和机器学习吸引了所有的注意力，因为它们帮助我们成功地解决了计算机视觉、自然语言处理等问题。这些用例是传统的基于规则的系统无法解决的，仅仅是因为所涉及的规则的庞大数量和复杂性，考虑到这些用例的输入中可能会有各种各样的变化。换句话说，如果我们必须手工编写准确识别所需的所有规则，输入空间通常非常巨大，并且接近无穷大。即使对于像 MNIST 这样的低变量数据集也是如此，更不用说 ImageNet 或其他场景了。

一般来说，神经网络是一个计算图，其中分类决策由针对训练数据优化的权重和偏差驱动，并且不显式地对决策应用逻辑推理。因此，任何非目标图像被错误地以更高的可信度分类为属于某一类并不令人惊讶。例如，每个像素可以有 256 个可能的值，因此，即使是 16×16 大小的小图像也可以有无限多的可能输入(即，256 个⁶* ⁶或~10⁶ ⁶可能图像)。考虑到如此大的输入空间，找出一些能使计算图产生与正常图像相同的结果并不奇怪。

## **4。如何生成对抗性的例子？**

从概念上讲，用于生成对立范例的方法与开发神经网络没有太大的不同。如果 A =训练数据，B =预期分类，C =模型权重，D =成本函数。在训练模型时，A 和 B 是固定的，我们不断改变 C 以确定使 d 最小的最佳值。类似地，为了生成如上所示的无针对性的对抗性示例，我们保持 B 和 C 固定，并不断改变 A 以确定使 d 最小的最佳值。

[这是 Pytorch 文档中的另一个例子](https://pytorch.org/tutorials/beginner/fgsm_tutorial.html),通过引入一个小的改变来产生一个有针对性的例子。

```
*# FGSM attack code*
**def** **fgsm_attack**(image, epsilon, data_grad):
    *# Collect the element-wise sign of the data gradient*
    sign_data_grad **=** data_grad**.**sign()
    *# Create the perturbed image by adjusting each pixel of the input image*
    perturbed_image **=** image **+** epsilon*****sign_data_grad
    *# Adding clipping to maintain [0,1] range*
    perturbed_image **=** torch**.**clamp(perturbed_image, 0, 1)
    *# Return the perturbed image*
    **return** perturbed_image
```

该文档提供了一个端到端的示例，包括模型定义、初始化和前馈方法，以及一个测试函数来运行攻击并可视化生成的对抗示例。但这一切的关键是上面的方法，创造了一个对立的例子。请注意，这与训练模型非常相似。通常，在针对给定输入和预期输出进行训练时，您会更新模型的权重。

```
*# Update weights*
    w1 **-=** learning_rate ***** grad_w1
    w2 **-=** learning_rate ***** grad_w2
```

然而在这里，权重没有改变，但是输入图像改变了。

```
*# Create the perturbed image by adjusting each pixel of the input image*
    perturbed_image **=** image **+** epsilon*****sign_data_grad
```

还要注意，在更新权重时，我们减去学习率乘以梯度，从而将它们向最小化成本函数的方向移动，而我们将ε乘以梯度添加到图像，从而向相反方向移动成本函数。

## **5。我们如何防御对立的例子？**

总的来说，还没有任何普遍接受的解决方案来抵御对抗性攻击。已经提出了许多防御技术，但结果不一，而且在随后的研究中经常被绕过。以下是一些重要的常见示例:

***对抗性训练*** 是在训练时使用对抗性的例子，以减少误分类。有不同的技术探索制定这一概念和改善培训。我们不会在这里讨论这种训练的各种技术和相关细节，但一般来说，对抗性训练在使模型对攻击具有鲁棒性方面产生了混合的结果。

***自动编码器*** 是使用的另一种机制。自动编码器是一种神经网络，它首先通过使输入通过一个较低维度的隐藏层来降低输入的维度，然后再尝试在其与输入层具有相同维度的输出层中重建信息。换句话说，它试图成为一个恒等式函数，只是它被约束为在重构信息之前首先压缩信息。根据定义，这消除了输入中的噪声，并且仅保留了重建原始图像所必需的那些特征。这种自动编码器也有助于消除敌对的干扰，并取得了一些成功。但是也可以使用前面描述的相同方法生成对立的例子，只是现在包括自动编码器以及网络的一部分。

*防御蒸馏是解决这个问题的另一种方式，正如这里讨论的[](https://arxiv.org/pdf/1511.04508v2.pdf)*和 [***这里的***](https://arxiv.org/pdf/1705.05264.pdf) 。防御性蒸馏是网络蒸馏的一种变体，其中网络的概率向量预测作为具有相同架构的蒸馏网络的训练标签。使用这样的软标签进行训练使得提取的网络平滑，对输入的变化不太敏感，并且对敌对输入具有鲁棒性。**

*****DeepSafe*** ，另一种很有前途的方法，就是这里讨论的[](https://arxiv.org/pdf/1710.00486.pdf)*。这是一种基于以下原则的技术，即输入空间的一个区域内的所有输入属于同一类，并且将被标记为相同。DeepSafe 首先将已知的标记输入分组到不同的聚类中，每个聚类包含相同类别的图像，并代表输入空间中的一个区域。然后，它发现在这个区域内是否有被不同分类的输入。如果在该区域内没有找到这样的输入，则认为它是安全的。如果找到一个，则重新绘制该区域并重复该实验，直到找到一个安全区域。***

***正如本文 中所讨论的 [***，也许对抗性的例子是不可避免的，尤其是在更高维度中更难防范。无论如何，这是一个重要的话题，对于参与这个领域的每一个人，从主管到爱好者，所有关于这个话题的研究和发展都应该被密切关注和尽可能的支持。***](https://arxiv.org/pdf/1809.02104.pdf)***