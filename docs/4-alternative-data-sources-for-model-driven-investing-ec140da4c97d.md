# 模型驱动投资的 4 个替代数据源

> 原文：<https://towardsdatascience.com/4-alternative-data-sources-for-model-driven-investing-ec140da4c97d?source=collection_archive---------10----------------------->

## 机器学习中超越股票价格的视角

![](img/52082a029c365fe7b63835ba8a326e84.png)

Photo by [Rabie Madaci](https://unsplash.com/@rbmadaci?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

机器学习的前所未有的崛起已经将其应用到许多行业，从航空旅行到医疗保健，从电子商务到物流，从保险到气象，甚至农业。投资领域也不例外，因为投资者所处的环境拥有丰富的数据。最近在金融预测中利用机器学习的许多尝试都集中在对时间序列价格数据采用复杂的深度学习技术，如[](https://en.wikipedia.org/wiki/Recurrent_neural_network)**(及其许多变体)，简单地说，这种方法使用过去的价格来预测未来的价格。没有对市场效率的先入为主的看法，这似乎是有道理的。价格是最可见和最容易获得的数据集之一，特别是对于股票，递归神经网络(RNNs)是专门设计来处理顺序数据的。然而，这种看似合适的结合很少产生样本外的预期结果。但是为什么呢？**

**价格数据中的信噪比低得令人难以置信，由于其可用性和普遍性，它长期以来一直被市场参与者所忽视。投资中有一个完整的子学科( [**技术分析**](https://www.investopedia.com/terms/t/technicalanalysis.asp) )，致力于在价格历史图表中寻找模式的深奥艺术。尽管这些方法不像 RNNs 那么复杂，但任何唾手可得的果实仍然会被套利掉。但这并不意味着量化投资完全没有用，如果机器学习模型是预测的引擎，那么数据只是它的燃料，如果价格不再足以作为合适的媒介，我们可以寻找其他来源来实现它的功能。如果你愿意努力寻找，仍然有许多免费的替代数据来源。**

# **去哪里找**

**![](img/9f0c911e47d6fe7f8deefa5caa1a74b1.png)**

**Photo by [Mamihery Razafindramamba](https://unsplash.com/@mamihery?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

**如果你是一个数据驱动的非机构投资者，无法访问彭博终端，但你想从雅虎导出价格时间序列升级到 csv！金融，下面的列表可能会引起你的兴趣:**

## **1.圣路易斯美联储银行**

**![](img/a55472ec07242238968abc785cb1390e.png)**

**Source:FRED, BEA**

**作为组成美国中央银行系统的 12 家地区储备银行之一，圣路易斯联邦储备银行始终掌握着美国经济的脉搏。除了在制定货币政策方面的重要作用，它还是宏观经济研究的中心。为了促进这项研究，它编制了美联储经济数据数据库，该数据库在一个地方汇集了 50 多万个不同的时间序列数据集。虽然该数据库主要存储国内和国际宏观经济数据，但它仍在不断扩展，新增加的内容包括比特币/加密货币价格指数。这里可以找到[](https://fred.stlouisfed.org/)**。****

****最近，为了协助实证研究，圣路易斯联邦储备银行发布了包含 100 个关键指标的月度和季度“大数据”数据库 [**弗雷德-MD 和弗雷德-QD**](https://research.stlouisfed.org/econ/mccracken/fred-databases/) 。这可能为你的财务预测问题提供了一个很好的起点。****

## ****2.卡格尔****

****![](img/7ee2d97f4b5513f2b2b17686e73b0cbb.png)****

****Photo by [Osman Rana](https://unsplash.com/@osmanrana?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)****

****[**Kaggle**](http://www.kaggle.com) 是世界上最大的在线数据科学社区，它也是一个机构发布数据相关问题的平台，让有抱负和经验证的数据科学家以类似竞赛的形式解决这些问题。用户不仅可以访问数据，而且顶尖的完成者通常会在结束后在网站博客上发布他们的方法、方法论和代码的详细说明。之前的获奖者包括 Geoffrey Hinton(通常被称为深度学习的教父)和他的学生。网站上有许多有趣的帖子，包括可用于数据驱动投资的替代数据。其中一个数据集来自著名的量化对冲基金 [**Two 适马**](https://www.kaggle.com/c/two-sigma-financial-news) 最近举办的一场比赛，在比赛中，你可以从汤森路透(Thomson Reuters)获得新闻报道，目的是预测股票价格。****

## ******3。Quandl******

****![](img/f599ffc96545d2821ae88a5dca90ba9f.png)****

****Photo by [Sam Beasley](https://unsplash.com/@sam_beasley?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)****

****Quandl 的 目标客户群是大大小小的投资者。凭借有趣的非传统指标，如前一周特定汽车的销量或苹果上个月的运营支出，Quandl 无疑提供了一种独特的产品。一些较难获得的数据集是收费的，但该平台确实免费提供大型市场和国际经济数据库。这可以通过 Excel、R 和 Python 的许多插件/API 来访问，因此可以很容易地集成到任何工作流中。****

## ****4.网页抓取****

****![](img/20b4adda6b95e088cabe1e565fed6b67.png)****

****Photo by [Christopher Burns](https://unsplash.com/@christopher__burns?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)****

****Web 抓取指的是从网页中提取数据，可以说这是可用的原始和非结构化数据的最大来源。有了像 R 中的 [**Rvest**](https://blog.rstudio.com/2014/11/24/rvest-easy-web-scraping-with-r/) 和 Python 中的 [**Beautiful Soup**](https://pypi.org/project/beautifulsoup4/) 这样的自动化网页抓取库的易用性和可访问性，只需四行代码就可以快速捕获、处理和存储网页的任何元素。正在使用的这种技术的有用例子包括 [**Lucca 和 Trebbi 2009**](http://www.nber.org/papers/w15367) ，其中来自美国国家经济研究局的作者在谷歌搜索中将美联储 FOMC 声明中的句子与“鹰派”和“鸽派”(用于表明央行对利率的立场的术语)结合起来，并捕获了返回结果的数量。这些结果随后被用来预测未来的利率轨迹。另一项相关的研究是 Preis、Moat 和 Stanley 2013 的研究，他们使用谷歌趋势分析来搜索特定的搜索词，以揭示股市不利波动的早期预警信号。还有许多其他的实际例子，但是你如何应用它以及在哪里应用它只受到浩瀚的互联网的限制。****

# ****结论****

****虽然我已经列出了 4 个可能有助于帮助你制定投资相关的机器学习问题的替代数据来源，但重要的是要注意，我们不能完全放弃价格的使用。最终回报是我们所追求的(至少对我们大多数人来说)，这是价格的函数。然而，在这种情况下，我们应该用价格来衡量结果，而不是投入的特征。从直觉上讲，这是有道理的，因为过去的价格不是影响股票的唯一因素，股票本质上是公司，而公司受制于其经营的商业和经济环境。****

# ******参考文献******

****卢卡博士和特雷比博士(2009 年)。测量中央银行沟通:应用于 FOMC 报表的自动化方法。 *SSRN 电子杂志*。****

****Preis，Moat h .和 Stanley h .(2013 年)。使用谷歌趋势量化金融市场的交易行为。*科学报道*，3(1)。****

******免责声明**:本帖纯属个人观点和看法的表达。它不代表任何建议，也不反映我的雇主的观点。****