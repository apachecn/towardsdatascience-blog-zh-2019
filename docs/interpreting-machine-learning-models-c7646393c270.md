# 如何解读机器学习模型？

> 原文：<https://towardsdatascience.com/interpreting-machine-learning-models-c7646393c270?source=collection_archive---------13----------------------->

## 我们能理解机器学习模型内部到底发生了什么吗？

![](img/683885108b0d69074868ae6c9015b5da.png)

Source: Photo by [Jeremy Thomas](https://unsplash.com/@jeremythomasphoto?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/data-science?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在我之前的[博客](http://datascienceninja.com/2019/07/01/the-balance-accuracy-vs-interpretability/)中，我谈到了模型性能和可解释性之间的权衡。通常，你会观察到商业利益相关者更喜欢不太精确但高度可解释的线性模型，因为它易于解释。但作为一名数据科学家，你知道在现实世界中，由于固有的高维数和特征之间复杂的非线性关系，非线性和复杂的模型总是更稳健和可靠。所以在一个理想的世界里，每个人都想在神圣的网格里，在那里你可以得到最高的模型性能和高度可解释的结果。

在这篇博客中，我简要地提到了我在项目中使用的一些技术，这些技术增加了可解释性，并解决了高模型性能和高可解释性之间的权衡问题。

![](img/b06fa55912eed0e88e22b84fea668711.png)

Source: [https://xkcd.com/1838/](https://xkcd.com/1838/)

以下是我用来增加模式可解释性的方法:

1.特征重要性:预测模型对特定特征的依赖程度？

2.部分相关图:特定特征如何影响模型预测？

3.Shap:哪些变量导致了这个预测？

4.莱姆:是哪些变量导致了这种预测？

为了解释上述方法，我使用了来自印度开放政府数据(OGD)平台——https://data.gov.in/[——的教育部门的数据集，该平台支持印度政府的开放数据倡议。这一数据包括辍学率、有电的学校百分比、计算机设施、厕所等。印度所有的邦。出于好奇，我想测试小学的辍学率是否与学校的设施有关。因此，我使用辍学率作为 y 变量(目标)，其他指标作为独立特征。](https://data.gov.in/)

**1。** **特征重要性:**

**基尼系数重要性或平均减少杂质**

对于分类问题，Scikit-learn 默认使用 Gini 杂质来计算特征重要性。特征重要性被称为“基尼重要性”或“平均减少杂质”。它被定义为集合中所有树的平均节点杂质的总减少量。通过到达特定节点的概率(在到达该节点的样本的总比例之外)对节点杂质的总减少进行加权。简而言之，这确保了如果“平均减少杂质”对于 2 个变量是相同的，但是变量 1 在树的顶部，而另一个在深度 5，那么变量 1 将变得更重要，因为与深度 5 的节点相比，它更容易到达该节点。因此，特性的值越高，它就越重要。最后，通过除以所有要素重要性值的总和，将要素重要性归一化到 0 和 1 之间。

下面是上述案例研究中的特征重要性图。

![](img/bd5db5df6de80d3f5afb4b9b9f22a824.png)

这表明，在印度各邦，小学辍学率受供电、供水和厕所设施的影响最大，而不是受电脑的影响。

**排列重要性**

置换重要性是计算特征重要性的替代方法，可用于任何模型。它基本上是一次一个特征，所有其他特征和目标保持不变。然后检查这如何影响重组数据中模型预测的准确性。因此，对于对预测影响最大的列，模型性能会降低。

![](img/9c3f37109dc4a6980500477e5f12ce8e.png)

在上表中，最重要的功能按重要性从高到低排列。权重列测量随机洗牌后模型性能(准确性)下降的程度。正如你所看到的，这两种方法中顶层变量的顺序是相同的，但这可能并不总是正确的。

**2。** **部分依赖情节(PDP)**

现在，特性重要性帮助我们解决了这个难题的一部分。但是为了知道每个变量如何影响预测，我们可以分析部分相关图。这可以帮助我们识别目标和特征之间的关系是线性的、单调的还是更复杂的。

在这种方法中，我们一次改变一个变量的值，其他特征和目标保持不变。有了这个我们就可以理解预测的结果是如何随着特定变量的变化而变化的。PDP 的逻辑非常简单，对于感兴趣的特征，它基本上在数据集中的所有数据点上强制一个单一值，然后在所有数据点上平均预测。对特定特性的所有值重复此练习。

![](img/4082c3a8d8e5cf807d5732bba8a897fe.png)

向下倾斜的图表表明，随着通电学校百分比的增加，辍学率与该特征的最小值相比有所下降。图表中的平坦区域表明，在这些区域中,%电力的增加不会导致辍学率%的任何变化。PDP 总是相对于特性的最小值进行测量，因此 y 轴上最左侧的点总是为零。蓝色区域表示不确定性。

您只需确保您正在分析的 PDP 的特征与数据集中的其他特征没有高度相关性。例如，在我们的数据集中，如果%有电的学校与%有电脑的学校呈正相关，那么当我们计算 PDP 时，将会有记录显示这两个特征的组合在现实中不太可能发生。如果在您的情况下，特征之间的相关性很高，那么您可以查找边际图和累积局部效应(ALE)图。

我将在接下来的博客中写关于莱姆和 SHAP 的内容。

请在评论中告诉我你对这个博客的想法。此外，我想知道您是否已经开发了来自印度开放政府数据(OGD)平台的案例研究。

这些内容最初发表在我的个人博客网站:[http://datascienceninja.com/](http://datascienceninja.com/)。点击[此处](http://datascienceninja.com/2019/07/10/how-to-interpret-machine-learning-models/)查看并订阅即时接收最新博客更新。