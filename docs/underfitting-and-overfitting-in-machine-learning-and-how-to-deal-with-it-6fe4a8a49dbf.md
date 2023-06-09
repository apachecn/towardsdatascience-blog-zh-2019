# 机器学习中的欠拟合和过拟合以及如何处理！！！

> 原文：<https://towardsdatascience.com/underfitting-and-overfitting-in-machine-learning-and-how-to-deal-with-it-6fe4a8a49dbf?source=collection_archive---------3----------------------->

![](img/5e4ee5296da0be2292e337c1f9496ee1.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

机器学习中模型性能不佳的原因是数据过拟合或欠拟合。

在这个故事中，我们将发现机器学习中的泛化概念以及随之而来的过拟合和欠拟合问题。

我们开始吧！！！

# 机器学习中的泛化

泛化指的是机器学习模型学习的概念在多大程度上泛化到模型尚未看到的特定示例或数据。

举个例子，假设我给你看一张猫的图片，让你给我“分类”；假设你正确地识别出它像一只猫，如果我把猫向左移动三个像素，你还能识别出它是一只猫吗？如果我把它翻过来呢？如果我把它换成一只不同品种的猫，你还能认出它吗？几乎可以肯定，所有这些问题的答案都是因为我们作为人类，我们以不可思议的轻松进行概括。另一方面，机器学习很难做到这些事情；它只在对一个特定图像进行分类时有效。

虽然机器学习可能能够在某个领域实现超人的性能，但除了它明确创建的领域之外，底层算法在任何其他领域都不会有效，因为它没有能力在该领域之外进行推广。从这个意义上来说，概括指的是智力的抽象特征，它使我们能够同时在数千个学科中发挥作用。

当我们谈论机器学习模型对新数据的学习和推广情况时，有一个机器学习中使用的术语，即过拟合和欠拟合。

过拟合和欠拟合是机器学习算法性能差的两个最大原因。

# 适合度

在统计学中，a 的**拟合优度**描述了它对一组观察值的拟合程度。

统计学通常描述拟合优度，它是指用于估计函数的近似值与目标函数匹配程度的度量。

# 过度拟合与欠拟合

我们可以通过观察相反的问题——欠拟合来更好地理解过拟合。

当模型过于简单(由太少的特征提供信息或太多的正则化信息)时，会发生欠拟合，这使得它在从数据集学习时不灵活。

简单的学习者倾向于在他们的预测中有较少的变化，但是更多偏向错误的结果。另一方面，复杂的学习者倾向于在他们的预测中有更多的变化。

**让我给你打个比方来解释过度拟合和欠拟合。**

过度拟合的模型就像主题专家:

他们对某个特定领域非常了解，例如主题专家。你问他们关于他们工具功能的任何问题(甚至是细节)，他们可能会非常准确地回答你。但是当你问他们为什么油价会波动时，他们可能会做出明智的猜测，并说出一些奇怪的话。

就机器学习而言，我们可以将它们表述为过于关注训练集(程序员)和学习复杂的关系，而这些关系通常对新数据(测试集)可能无效。

不称职的模特就像那些想成为板球运动员但被父母强迫从事工程的工程师。他们对工程和板球都不太了解。他们对自己所做的事情从来都不感兴趣，对所有的事情都没有足够的了解。

就机器学习而言，我们可以说它们对训练集关注太少。既不适合培训也不适合测试。

# 如何检测欠拟合？

当一个模型试图建模的数据过于简单时，它就不适合。

检测这种情况的一种方法是使用[偏差-方差法](http://en.wikipedia.org/wiki/Bias%E2%80%93variance_dilemma)，它可以表示为:

> 当你有一个高偏差时，你的模型是不适合的。

# 如何避免不合身:

更多的数据通常不会有帮助。事实上，这可能会增加训练误差。因此，我们应该增加更多的功能。因为这扩大了假设空间。这包括从现有要素创建新要素。同样，更多的参数也可以扩展假设空间。

# 如何检测过度拟合？

过度拟合和一般机器学习的一个关键挑战是，在我们实际测试之前，我们无法知道我们的模型在新数据上的表现如何。

为了解决这个问题，我们可以将初始数据集分成单独的*训练*和*测试子集*。这种方法可以估计我们的模型在新数据上的表现。

**如果我们的模型在训练集上比在测试集上表现得更好，那么我们很可能过度拟合了。**

例如，如果我们的模型在训练集上有 95%的准确率，但在测试集上只有 48%的准确率，这将是一个很大的危险信号。

# 如何防止过度拟合

检测过度拟合是有用的，但不能解决问题。幸运的是，您有几个选择可以尝试。

以下是一些最流行的过度拟合解决方案:

*   **交叉验证:**找出样本外预测误差的标准方法是使用 5 重交叉验证。
*   **提前停止:**它的规则为我们提供了在学习者开始过度适应之前可以运行多少次迭代的指导。
*   **剪枝:**剪枝在构建相关模型时被广泛使用。它只是删除了对当前问题没有多少预测能力的节点。
*   **正则化:**它引入了一个代价项，用于在目标函数中引入更多的特征。因此，它试图将许多变量的系数推至零，从而减少成本项。
*   **移除特征:**有些算法内置了特征选择。对于没有概化的要素，您可以通过移除不相关的输入要素来手动提高它们的概化能力。一个有趣的方法是讲述一个关于每个特性如何适应模型的故事。这就像数据科学家在软件工程师的橡皮鸭调试技术上的旋转，他们通过对橡皮鸭逐行解释来调试代码。
*   **用更多的数据训练:**不是每次都管用，但是用更多的数据训练可以帮助算法更好的检测信号。在早期的儿童身高与年龄模型的例子中，很明显采样更多的学校将有助于你的模型。当然，情况并不总是这样。如果我们只是添加更多的噪声数据，这种技术不会有帮助。这就是为什么您应该始终确保您的数据是干净的和相关的。
*   **集成:**集成是用于组合来自多个独立模型的预测的机器学习方法。有几种不同的组装方法，但最常用的两种是:

***装袋*** 试图减少复杂模型过拟合的机会。

*   它并行培养了大量的“强”学习者。
*   强学习者是一种相对不受约束的模式。
*   Bagging 然后将所有强学习者结合在一起，以便“平滑”他们的预测。

***Boosting*** 试图提高简单模型的预测灵活性。

*   它按顺序训练出大量的“弱”学习者。
*   弱学习者是一个受约束的模型(也就是说，你可以限制每个决策树的最大深度)。
*   序列中的每一个都着重于从之前的错误中学习。
*   然后，Boosting 将所有弱学习者组合成一个强学习者。

虽然 bagging 和 boosting 都是整体方法，但它们从相反的方向处理问题。

Bagging 使用复杂的基础模型，并试图“平滑”他们的预测，而 boosting 使用简单的基础模型，并试图“提高”他们的总体复杂性。

如果你想了解更多关于集合模型的知识，集合模型的重要技术:bagging 和 boosting。请在下面的链接中浏览我以前的故事。

[](https://medium.com/@sainikhilesh/difference-between-bagging-and-boosting-f996253acd22) [## 装袋和助推的区别？

### 装袋和助推是全球各种数据爱好者常用的术语。但是到底装袋和…

medium.com](https://medium.com/@sainikhilesh/difference-between-bagging-and-boosting-f996253acd22) 

我希望这篇文章能让你对这个话题有一个坚实的理解。在这篇文章中，你已经了解了机器学习中过度拟合和欠拟合的泛化术语。

你有任何关于过度合身、不够合身或与这篇文章相关的问题吗？留下评论，提出你的问题，我会尽力回答。

感谢阅读！❤