# 数据样本和错误可视化技术

> 原文：<https://towardsdatascience.com/data-samples-and-error-visualization-techniques-832c4a7fbcb2?source=collection_archive---------17----------------------->

![](img/80eb72e7843c78857a454beeb0413a72.png)

## 为什么在构建数据可视化时，我们应该选择有代表性的样本，并考虑到误差。不确定条形图和不确定排名列表的简要概述。

填充我们的可视化的数据样本的类型会给我们的结果增加不确定性。一些常见的数据显示方式，如条形图和饼图，比其他方式更能让人们理解这种不确定性。本文探讨了如何理解我们的数据样本，并创建最合适的图形来可视化它们所代表的内容。

一般来说，数据科学的目标是理解数据并生成预测模型，以帮助我们做出更好的决策。有关数据可视化的更全面概述，请参见“[数据可视化和真实艺术](/data-visualization-and-truthful-art-324b13a2ad34)”

# 了解您的数据集

在数据分析中，我们经常处理小样本，而不是全部数据。完整的数据集可能会因为计算的简化而减少，或者因为只有一个更复杂的数据世界的小子集可用。在这种情况下，数据科学家通常会创建忽略样本真实性质的可视化效果。有时他们甚至没有意识到他们的数据集只是一个样本。

当我们基于小数据集创建分析时，需要考虑不确定性。但在许多情况下，这种情况不会发生，因为包含不确定性和统计复杂性会导致更复杂的过程，从而降低整体分析的速度。但是每当我们优先考虑快速迭代和探索而不是统计准确性时，我们需要意识到我们正在这样做。

# 视觉数据分析和不确定性:一个古老的二分法

没有多少标准的可视化技术以直观的方式拥抱不确定性，并使不确定性范围易于理解。图 1 中的例子用概率可视化演示了这个问题。

![](img/571be4f0a86436ae1c304dd06cb22831.png)

Figure 1

# 不确定性问题

比较条形图中两个条形的高度是微不足道的。但是很难计算几乎重叠的不确定区域的概率。即使是受过统计学训练的专家在解释置信区间时也会出错。

不确定性必须用不同的心态来计算。我们需要问的不是 A 是否大于 B，而是 A 大于 B 的概率是多少。这种模糊逻辑包含了现实生活中的不确定性。数据可视化应该符合这种范式。

根据“不确定性下的判断:启发式和偏见”，人们在分析不确定数据时往往会做出错误的决定(Tversky 和 Kahneman 1974)。我们的大脑没有以直观的方式处理概率数据的能力。为了解开这个问题，我们首先需要清楚地想象两件基本的事情:

*   置信区间
*   样本大小信息

## 如何可视化不确定性

我们都熟悉的经典可视化并不是创造不确定性的深刻展示的好方法。好的可视化不仅仅是从表格或文件中复制数据。它以可视化格式显示相关数据，揭示趋势或关系。当洞察力被成功可视化时，观众会“啊哈！”瞬间。

即使是专家也很难在阅读置信水平以外的任务中使用置信区间。尽管这很复杂，但对不确定性的正确描述有助于我们理解决策过程的风险和价值。

## 实际例子

当我们处理样本时，我们只能估计数据的总体情况。例如，基于样本的数据集的预期平均值、总和或计数。我们可以推断出这个期望值的分布。根据“带控制的交互式数据分析”，我们可以使用*中心极限定理*根据这些估计量来估计误差界限(Hellerstein et al. 1999)。

图 2 中的图表基于一个大型销售数据集的样本。置信区间为 95%。所以我们预计 1995 年的平均销售额在 49，000 英镑到 51，300 英镑之间。

![](img/1744adc74ed4bf476cfd7d0971ae0457.png)

Figure 2

这些任务通常在数据分析的探索阶段完成:

*   求最小值和最大值。
*   对值进行排序。
*   比较值。

在常规图表中，如果没有不确定性，这些任务就像比较值或检查 A 条是否大于 b 条一样简单。然而，当我们接受不确定性和概率分布时，就没那么简单了。在这些情况下，我们需要根据给定的分布进行统计推断。同样，处理这种模糊逻辑需要改变思维方式。也就是我们不能问某个事实是不是真的。我们只能估计一个事实是真实的可能性。

接下来，我们将探索两种可视化技术:不确定性条形图和排序列表。

## 不确定性条形图

在“面向样本的任务驱动可视化:让用户做出更好、更自信的决定”中，作者讨论了基于不确定条形图的五个任务(Ferreira 等人，2014 年):

*   比较一对杠。
*   求最大值或最小值。
*   将值与常数进行比较。
*   将值与范围进行比较。

图 3 比较了白色条和其他条:深蓝色表示*肯定低于*，深红色表示*肯定高于*。

![](img/dd01de1dbdf1e0302ba0c1b61e004bda.png)

Figure 3

图 4 显示了最大值和最小值。这两个饼图显示了任何给定棒线可能是最大值或最小值的概率。

![](img/6b5b81b6ce32572669cd790bc1895b33.png)

Figure 4

图 5 比较了一个条形和一个固定值。在这种情况下，很容易计算图表高于或低于固定值的概率。

![](img/80b2a307ad0c5b813024b8be8a9e894b.png)

Figure 5

在图 6 中，深色的*可能在范围*内，浅色的*在范围*外。

![](img/ab742bfa8f45191d0d1a9306b91d74e2.png)

Figure 6

## 不确定排名列表

*常规排序列表*代表排序后的元素。它们通常只显示一大组变化中顶部的几个小节。例如，我们可能希望可视化服务器日志中最常发生的前五个事件。为了获得这些信息，我们需要对所有的值进行排序并截断列表。当可能值的数量太大而无法显示时，这种方法非常有效。

它们在不稳定的环境中非常有用，在这种环境中，新值会随着时间的推移变得更加相关。这种列表类型趋于稳定，但支持快速变化。

*不确定排名榜*有偏序。我们确信有些项目会比其他项目更大。但是我们可能不确定其他的成对关系。在他们的可视化文章(Ferreira 等人，2014 年)中，作者探讨了基于排序列表的两个任务:

*   确定哪些项目可能会落在给定的等级上。
*   确定哪些项目可能落在给定的一对排名之间。

Ferreira 等人(2014 年)还设计了两步算法来计算不确定性:

> 1-作为一种启发式方法，**中心极限定理**被用来根据我们到目前为止看到的项目的计数、标准偏差和移动平均值来估计置信区间。使用这种技术，作者为图表上的每个聚集创建一个分布。
> 
> 2-***蒙特卡罗方法*** 用于计算概率，依赖于计算出的分布。

每个任务由一个谓词表示。也就是说，D1 很可能比 D2 更强大。Ferreira 等人(2014 年)从每个分布中反复抽取样本，并根据样本评估谓词。他们重复这个过程大约 10，000 次。事件的概率是谓词为真的迭代的分数。这种计算方法只计算近似概率。但是如果我们运行它很多次，它会产生精确的近似值。

图 7 是用分级列表而不是条形图显示的相同数据的表示。

![](img/c39a70af0083e9ae65e362af8bc5afbd.png)

Figure 7

我们可以通过使用这种可视化来完成这两项任务:

1-确定在给定等级下哪个项目可能会下降(图 8 中的前 3 位)。

![](img/548adcf62df8d621246decc8d44984e4.png)

Figure 8

2.确定哪些项目可能落在给定的一对排名之间(图 9)。

![](img/c6679f3abf131d6b249722aa22ec8749.png)

Figure 9

高度、宽度和颜色与该物品落入该箱的概率成比例。几乎可以肯定，1992 年和 1993 年会落在前三项。1994 年和 1995 年瓜分剩下的。

# 用户测试后的结论

Ferreira 等人(2014)的研究表明，条形图可以带来更直观、更深刻的分析。因此用户在解释数据时不太可能出错。然而，使用特定于任务的注释来增强条形图可能会帮助用户对他们的样本做出更好的决策。

# 参考

n .费雷拉、d .费希尔和 A.C .柯尼希(2014 年 4 月)。"面向样本的任务驱动可视化:允许用户做出更好、更自信的决策."可用[此处](https://www.researchgate.net/publication/266655543_Sample-oriented_task-driven_visualizations_Allowing_users_to_make_better_more_confident_decisions.)。

Figueroa，A. (2019)“数据可视化和真实艺术”.*走向数据科学*。可用[这里](/data-visualization-and-truthful-art-324b13a2ad34.)。

Hellerstein，j .，Avnur，r .，Chou，a .，Olston，c .，Raman，v .，Roth，t .，Hidber，c .，和 Haas，1999 年 8 月)。"交互式数据分析与控制." *IEEE 计算机*，32(8)，51- 59。此处[可用](http://control.cs.berkeley.edu/ieeecomputer.pdf)。

Olston 和 j . Mack inlay(2002 年 7 月)。"可视化具有有限不确定性的数据." *IEEE Symp。关于信息可视化* *(INFOVIS 2002)* 。第 37-40 页。此处可用[。](https://www.researchgate.net/publication/2951574_Visualizing_Data_with_Bounded_Uncertainty)

特沃斯基和卡尼曼(1974 年 9 月)。"不确定性下的判断:试探法和偏见."*理科*，185。1124–1131.此处可用[。](https://www.ncbi.nlm.nih.gov/pubmed/17835457)