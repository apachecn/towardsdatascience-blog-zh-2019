# 我们观察的角度

> 原文：<https://towardsdatascience.com/the-angles-from-which-we-see-582c5cb5ec75?source=collection_archive---------23----------------------->

## 向非技术观众揭开 PCA 的神秘面纱

想象你是一个艺术家，想在一张纸上画一栋房子。这个任务的本质是将一个物体从 3D 世界转换到 2D 平面。

如果你可以在这个房子里自由走动，你会选择哪个角度来画画？

![](img/bb220f515c2e2046f129928debbb2e23.png)

Two different angles to look at the house

我们想要的是画房子的最佳角度，以这种方式可以很好地捕捉到关于这个房子的最重要的信息——如窗户的位置、高宽比。因此，我们可能会选择从左图所示的角度将房子“投影”到纸上，而不是右图所示的角度。

在机器学习中，我们处理类似的问题。

真实世界的数据集通常有太多的维度(特征)而无法有效地可视化。例如，客户的购买行为可以归因于许多因素，如收入、年龄、社会价值观等等。这些因素中的每一个都会在数据集中给出一个新的维度。

然而，人类很难在视觉上想象一个超过 3 维的数据集。因此，为了让领域专家查看数据并从中提取有意义的结论，我们通常需要将数据集缩减为几个主要部分。

这个降维的过程可以通过**主成分分析(PCA)** 来实现，这是一种在无监督学习中广泛使用的方法。

举例来说，我们看一个二维数据集，如下图所示，在 x-y 平面上，看看我们如何将它简化为一维，即一条线。

![](img/1fd11ed967f399f1ecd1c446f7112db0.png)

Two angles to project the data onto a line

从数学上来说，有不同的方法找到正确的投影。本质上，我们在寻找一条到所有数据点的平均(均方)距离最小的直线。通过选择左边的线，数据的大多数变化将被保留在新的维度中。

因此，主成分分析的核心思想是找出我们投射数据的最佳角度。

在实际使用案例中，这可能意味着将要素总数从数千个减少到数百个，从而显著缩小数据集。然而，在这里，我们将看一个关于客户定位的相当简单的用例。

假设我们想要了解我们的客户，以获得对我们提供的产品推荐类型的洞察力。一种可能是查看他们的购买记录，以了解他们购买行为背后的个人特征。我们可能会得出这样的结论:一些客户更注重价格，一些客户更快地采用技术。

![](img/12aba95b7833a59a601bfcfeb1239f6a.png)

Customers’ speed for tech adoptions vs price sensitivity

直觉上，客户对价格的敏感度和技术采用的速度可以降低到一个维度，在某种程度上捕捉客户对高科技公司的整体吸引力。因此，我们可以在新的红线上表示每个客户，其中位于红线右侧的客户比位于左侧的客户更有吸引力。

![](img/dbcc83969a56a2872e2395c57d007f50.png)

*Customer attractiveness = weight1* × *p + weight2* × *t + c*

一般来说，每个主成分都是原始特征的线性组合。同样，这里的客户吸引力是价格敏感度(p)和技术采用(t)的加权和，再加上一些常量值(c)。

在我们生活的复杂世界中，我们不断地选择正确的角度来看待事物。从某些角度来看，我们感知到一些有意义的东西，而从另一些角度来看，我们没有。

就像艺术家选择一个角度来画一栋房子一样，PCA 是关于选择我们看到的那个直角。