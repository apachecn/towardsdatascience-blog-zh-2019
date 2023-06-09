# 如何用强大的临床研究工具征服队列分析

> 原文：<https://towardsdatascience.com/how-to-conquer-cohort-analysis-674a2dea3472?source=collection_archive---------25----------------------->

## 为什么你的医生比你更了解客户维系

![](img/54ce54c8e0b7ca61a44fe4e4ea8ff49a.png)

在 SaaS 或消费者订阅环境中，客户流失的微小变化会从根本上影响收入增长。

产品经理、增长黑客、营销人员、数据科学家和投资者都需要了解商业决策如何影响用户留存。

随着如此多的经常性收入业务上市，硅谷*现在应该*了解情况了。

然而，信不信由你，**医学研究人员比你更擅长衡量客户保持率。**

什么？

听起来很大胆，但事实并非如此。几十年来，临床研究人员已经提炼出精确而严谨的方法来衡量保留率——只不过他们衡量的不是*客户*保留率，而是*患者存活率*。

生死的严重性意味着研究人员在衡量治疗效果时非常小心。

为此，临床研究人员使用一种叫做 [**卡普兰-迈耶估计量**](https://en.wikipedia.org/wiki/Kaplan%E2%80%93Meier_estimator) 的统计方法。该公式巧妙地解决了队列保持分析中经常出现的一个问题:**在不同寿命的队列组内部和之间进行有效的比较**:

![](img/08fe9d5e3309d7d1296feb772b50ede7.png)

尽管公式很花哨，但使用 Kaplan-Meier (KM)的生存分析实际上非常简单，并且比其他方法提供了更好的结果:

![](img/0849ede77b317bf1fa9196ddaf7c5355.png)

在这篇文章中，我将解释这些结果，用简单的术语分解 KM 估算器，并说服你用它来进行保留分析。

底线:**如果你是一名经营者或投资者，想要恰当地衡量客户群保持率，那么卡普兰-迈耶是一个不错的选择。**

# 两个必然:死亡和流失

KM 估算器帮助我们处理的核心问题是**缺失数据**。

队列数据本身就有缺陷，因为最近的队列与老队列相比数据点更少。例如，一个五个月大的队列只能与一个十个月大的队列的前五个月进行比较。七个月前获得的客户群的保留率只能合理地与前七个月老客户群的保留率进行比较。

假设您有前 12 个月的完整保留历史，并且您想要预测新获得客户的 12 个月保留曲线。怎么做一点都不明显。

为了更好地理解这一点，让我们想象一个只有五个群组的简单例子:

![](img/7b0114c54c22b8d521a36d3882376190.png)

你可以先试着计算不同群体的平均保持率。这是有问题的，原因有二:

*   如果我们的队列大小不同，简单的平均值就不具有代表性
*   对于任何给定的月份，我们只能对至少存活了这么长时间的群体进行平均，因此随着时间的推移，我们实际上对越来越少的群体进行平均

下面可以看到第二期。无论是简单平均值还是加权平均值，当表现在群组间波动时，我们都会得到奇怪的结果:

![](img/26d99f3c71ffb828a6b78fc920079650.png)

假设我们不重新添加之前涌入其原始群体的返回用户，那么在下降后，保留率不可能上升——这是一条单行道。这是我们有缺陷的方法的产物，因为根据定义，5 个月的保留期不能超过 4 个月。

第三个相关的问题出现在将一组群组与其他群组进行比较时，例如，将 2016 年的每月群组与 2017 年的群组进行比较。正如我们刚刚展示的，使用平均值来估计每个群组的保留曲线是行不通的，这意味着我们也无法将一个群组与另一个群组进行比较。

# 有问题吗？问问你的医生

![](img/1643a46482870ffc5be3c0d2df3b553e.png)

信不信由你，临床研究人员一直在处理同样的问题。

客户群类似于在不同时间开始治疗的患者群体。这里的“治疗”是获得客户的时间，“死亡”只是流失。

或者，想象一下，如果“2016 年队列”和“2017 年队列”，而不是按年份分组的队列，是在临床试验中接受不同治疗的群体。我们想量化两组患者存活率(客户保持率)的差异。

制药公司和其他研究机构经常面临这一问题。患者在不同的时间开始治疗。患者因死亡而退出研究，但也因搬家或决定停止服药而退出研究。

这在任何患者的临床试验记录的开始、中间和结尾都造成了大量的数据缺失问题，使有效性和安全性的分析变得复杂。

为了解决这个问题，1958 年，数学家[爱德华·卡普兰](https://en.wikipedia.org/wiki/Edward_L._Kaplan)和统计学家[保罗·迈耶](https://www.chicagotribune.com/news/ct-xpm-2011-08-18-ct-met-meier-obit-20110818-story.html)，共同创建了[卡普兰-迈耶估计量](https://www.tandfonline.com/doi/abs/10.1080/01621459.1958.10501452)。也被称为*乘积限估计器*，该方法有效地处理了缺失数据问题，提供了对任何一点的生存概率的更精确的估计。

[卡普兰-迈耶背后的核心理念](http://biostat.mc.vanderbilt.edu/wiki/pub/Main/ClinStat/km.lam.pdf):

> *到任何时间点的估计存活概率是每个先前时间间隔的累积存活概率，计算为先前存活概率的乘积*

上面那个奇怪的公式只是简单地将一堆概率彼此相乘，以找到在某一点上生存的累积概率。

这些概率从何而来？**直接来自数据**。

KM 表示，我们对从一个月到下一个月的生存概率的最佳估计正是我们数据集中该月的加权平均保留率(在统计学术语中也称为 [*最大似然估计器*](/a-gentle-introduction-to-maximum-likelihood-estimation-9fbff27ea12f) )。因此，如果在一组群组中，我们有 1000 个客户从第一个月开始，其中 600 个存活到第二个月，我们对从第一个月到第二个月存活的“真实”概率的最佳猜测是 60%。

下个月我们也这样做。将第 3 个月存活的客户数除以第 2 个月存活的客户数，得到第 2 个月到第 3 个月的估计存活概率。如果我们没有一个群组的第 3 个月的数据，因为它只有两个月大，我们从我们的第 3 个月生存计算中排除这些客户。

重复尽可能多的群组/月份，在每次计算中排除当前期间的任何群组缺失数据。然后，要计算任何给定月份的生存概率，将该月份的个人月度([条件](https://www.khanacademy.org/math/statistics-probability/probability-library/conditional-probability-independence/v/calculating-conditional-probability))概率相乘。

虽然这是一种病态的想法，但是测量患者存活率在功能上等同于测量客户保持率，因此我们可以很容易地将知识管理转化为客户群组分析！

# 测试卡普兰-迈耶

让我们通过将 Kaplan-Meier 估计量应用到前面的例子中来更清楚地说明这一点。

![](img/c8a2291a226997662ec4ef24a781e962.png)

第 1 个月存活的概率是 **69%** (第 1 个月存活的客户总数除以第 0 个月的总数)。假设客户在第 1 个月存活，则第 2 个月存活的概率为 **72%** (第 2 个月存活的客户总数除以第 1 个月的总数，不包括缺少第 2 个月数据的最后一组客户)。所以至少存活两个月的累计概率是 69% x 72% = **50%** 。冲洗，洗涤，然后每个月重复一次。

并排比较揭示了 KM 的优越性:

![](img/96862c47ea5f43370ad8ca68ac153c4a.png)

知识管理的伟大之处在于它利用了我们拥有的所有数据，甚至是我们观察较少的年轻群体。例如，虽然第 3 个月时所有可用群组的平均值仅使用群组 1-3 的数据，但由于其累积性，KM 估计值有效地纳入了较新群组的早期保留。这产生了 38%的 3 个月保留率估计值，高于我们在第 3 个月实际测量的任何群组。

**这正是我们想要的**-第 4 组和第 5 组都比第 1 组和第 3 组更大，也更容易保持。因此，从这些群组中随机挑选的客户的 3 个月保留率很可能会超过历史平均水平，因为该客户很可能在群组 4 或 5 中。

使用所有的数据也很好，因为这使得我们对尾部概率的估计比我们只依赖我们保留了那么久的客户数据要精确得多。

卡普兰-迈耶曲线还通过遵守[概率基本定律](https://www.investopedia.com/terms/c/compound-probability.asp)修正了留存曲线右尾的不稳定行为:累积概率只会随着数字的增加而下降。

# 95%的医生推荐

这种分析很容易扩展。让我们回到 2016 年与 2017 年的例子——我们可以对每一组队列进行卡普兰-迈耶计算，然后比较所得的生存曲线，突出两组之间预期保留的差异。

虽然我不会在这里讨论，但是你也可以计算卡普兰-迈耶曲线的 [p 值、置信区间和统计显著性检验](https://math.unm.edu/~james/w4.pdf)。这让你可以做出严格的陈述，如“2018 年相对于 2017 年的队列保留率的改善具有统计学意义(在 5%的水平)”-酷的东西:

![](img/d34df04b9b597f51e3f9560673d872bf.png)

对于那些花时间分析客户群体数据的人来说，Kaplan-Meier 是一个强大的工具。知识管理已经在严格的临床试验中经受了考验——如果说有什么不同的话，那就是它没有在技术运营商和投资者中更受欢迎。

如果你是一名产品经理、增长黑客、营销人员、数据科学家、投资者或任何其他理解客户保持分析的重要性的人，卡普兰-迈耶估算器应该是你的分析武库中的一件有价值的武器。

*最初发表于*[*https://whoisnnamdi.com*](https://whoisnnamdi.com/how-to-conquer-cohort-analysis/?utm_source=medium&utm_medium=article&utm_campaign=launch)

*在* [*推特*](https://twitter.com/whoisnnamdi) *上关注我，听听我对科技商业和经济的看法。*