# 机器学习！= .适合()

> 原文：<https://towardsdatascience.com/machine-learning-fit-de943469cc19?source=collection_archive---------14----------------------->

像所有初学者一样，当我开始机器学习之旅时，我犯了太多的错误。这是同样的故事。要学的东西很多。大肆宣传。大量的技术术语。涵盖了大量的先决条件等等。

似曾相识？我知道。

![](img/b61321d099b9243de5077209bf95b5a8.png)

Photo by [David Paschke](https://unsplash.com/@davidpaschke?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

对我来说，当时机器学习只涉及复杂的数学，没有别的。都是关于越来越复杂的模型。我在学习所有的数学细节，并欺骗自己我正在学习，但事实上，情况并非如此。

当时我脑海中有一个事实上的规则，如果你想提高性能或减少误差指标，就切换到更复杂的模型。并且一直做下去，直到性能提升或者损耗降低。

说说结果？**挫败感！**

事情没有按照我的期望进行。在从线性回归切换到具有 RBF 核的支持向量机回归机之后，我一直在等待性能大幅提升。

但现实世界中事情并不是这样的。

这样做了很多次后，我意识到这里有什么地方出了问题，我需要找出原因。

> **我了解到:**
> 
> **垃圾进= >机器= >垃圾出**
> 
> **机器学习！= .fit()**

不要犯同样的错误。

机器学习还有很多东西。

不仅仅是复杂的模型。不仅仅如此。

以下是机器学习流程中你也应该关注的三个主要步骤:

# **数据清理**

在现实世界的项目中，你不会每次都得到那个干净的`.csv`文件。更常见的情况是，您必须从多个来源收集数据，清理它们，然后连接它们，并进一步检查一致性和重复。

数据清理不仅仅涉及填充缺失值。除此之外还有很多事情。下面列出了其中的一些:

*   **检查整个数据的一致性**
*   **选择与您的问题相关的数据子集。**
*   **异常值处理**

剔除离群值不是解决办法。有时，您需要深入挖掘，找出这个记录值行为不同的原因。根据你的问题陈述，在真实案例中可能吗？然后，进行相应的处理。

*   **重命名列名以提高可解释性**
*   **删除重复记录**
*   **处理缺失值**
*   **以正确的格式存储抓取的数据**

还有更多…

# 数据分析和可视化

如果你不了解你的数据，你就不能用它做任何事情。当然

询问与业务问题相关的问题，并通过代码了解解决方案。有时，在现实世界中，任务不是建立一个最先进的模型来预测一些事情。而是分析数据，找出隐藏的可以让业务受益的洞察，用简单的语言把洞察呈现出来。

例句:假设你在亚马逊工作，你知道客户在平台上进行的每笔交易的大部分细节。

你可以问的问题:

1.  一天中大多数交易发生的高峰时间是什么时候？
2.  亚马逊上卖得最多的是什么类型的产品？
3.  收视率多少对购买有影响吗？

还有更多…

明白了吗？你的目标是找出可以帮助亚马逊获得更多销售的见解。

你的问题随着你的问题陈述的改变而改变。

即使你的目标是预测某事，如果不知道你的数据，你也不能做得很好。

不仅如此，数据分析和可视化还有助于您进行下一步工作，即特征工程

为什么大家都说:**认识你自己，背后是有原因的。**

# 特征工程

它是从原始特征集中提取新特征或转换现有特征集以使其适用于机器学习模型的过程。

**为什么选择特色工程？**

你需要明白:**具有良好特性集的简单模型比具有不良特性集的复杂模型表现更好。**

不理解数据和你的问题陈述，你就不能进行特征工程。

领域知识在特征工程中起着非常重要的作用。你需要找出以前在这个空间里做过的工作。阅读文献，然后结合你的发现构建新的特征。如果你有这个闲心，最好和领域专家谈谈。

**特征选择**:从原始集合中选择重要特征的子集。它也属于特征工程，sklearn 有关于它的大量文档。在这里 看完 [**。**](https://scikit-learn.org/stable/modules/feature_selection.html)

创建一个简单的基线模型，这样你就可以在加入新特性后比较你的结果，看看它们是否有帮助。记住:**这是一个迭代的过程**。

投入时间构建新特性远比等待一个复杂的模型开始工作要好。

关键教训:不要爱上复杂的模型，而要爱上数据。各有侧重。都是有联系的。

希望你喜欢这篇文章，并学到一些新东西。将这些知识融入到你的新项目中，并与刚刚起步的人分享这篇文章！

关注我更多这样的文章。和平与力量。