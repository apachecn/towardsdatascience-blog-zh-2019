# 金融科技初创公司数据新闻实习生的 3 课

> 原文：<https://towardsdatascience.com/3-lessons-from-a-data-journalism-intern-at-a-fin-tech-startup-c765817f3299?source=collection_archive---------21----------------------->

## [现实世界中的数据科学](https://towardsdatascience.com/data-science-in-the-real-world/home)

## ***了解我在一家金融科技初创公司实习时学到的经验，这家公司正在利用机器学习来彻底改变信贷承销行业。***

![](img/66f06383edde6114f9cf6e3102cc05d9.png)

The Data Science Team at ZestFinance (I’m on the upper left corner!)

随着我们进入秋季，我想我应该花时间反思一下我在加利福尼亚州洛杉矶 Zest Finance 担任数据记者的 14 周暑期实习。

如果你不熟悉我的背景，我目前是一名硕士研究生，正在进入研究生院的最后一年，学习计算机科学。我是怎么在 ZestFinance 结束的？我在网上申请，招聘人员发现我的经历很有趣，经历了面试过程，最终接受了邀请，作为 12 名实习生之一去他们的办公室过暑假。

我的目标是分享我从这次难忘的经历中学到的一些重要经验。

## **什么是 ZestFinance？**

该公司的使命是让每个人都能获得公平透明的信贷。根据[公司网站](https://www.zestfinance.com/about):

*数万亿美元的贷款行业仍然依赖陈旧的评分技术，这种技术过于简化了对借款人财务状况的看法。结果，数百万本应得到贷款的人总是被拒绝。大约 4600 万美国人要么是“信用隐形人”，在三大信用机构之一没有档案，要么是“不可记录的人”，没有足够的信息来产生信用评分。这是现代信用体系的失败。*

*基于机器学习的信贷模型可以通过从更多数据中获取更深入的见解，特别是银行已经拥有的未使用的数据，来产生更有利可图的承保。ZestFinance 是首批部署机器学习模型进行借贷的公司之一，我们知道它是可行的。*

![](img/8d74c2dc9c31cce562158dc13bcd8681.png)

## **Zest 的自动化机器学习(ZAML)**

更具体地说，我整个夏天都在研究 Zest 专有的自动化机器学习平台 ZAML。ZAML 使贷方能够分析非传统数据，包括他们内部已经拥有的数据，如客户支持数据、支付历史和购买交易。该平台还可以考虑传统的信用信息和非传统的信用变量，如客户如何填写表格，他们如何浏览贷款人的网站等。虽然黑盒问题减缓了机器学习在消费金融中的应用，但 ZAML 能够全面解释数据建模结果，衡量业务影响，并符合监管要求。

作为一名数据记者，我是数据科学团队中值得骄傲的一员。更具体地说，我的职责包括:(1)从大型和小型数据集挖掘趋势和见解，以讲述数据故事，(2)利用内部和外部数据源进行分析、建模和可视化，并将它们转化为主题叙述、报告和白皮书，以及(3)宣传数据科学研究计划，同时与营销团队跨职能合作，以量化其不断增长的影响和相关性。

现在你对团队和我的角色有了更多的了解，让我们深入了解一下我从这次实习中获得的一些主要见解。

## **最小可行分析**

这个概念来自[](/mva-minimum-viable-analysis-63b1e838ca08?sk=a2a8581eb5008d8b29c10e3dbf5500d7)[康纳·杜威](https://medium.com/u/ee856fa71ed0?source=post_page-----c765817f3299--------------------------------)的一篇优秀文章，我整个夏天都在回想这个概念([查看我对他的采访！](https://datacast.simplecast.com/episodes/conor-dewey))。这篇文章谈到了**最小可行分析**的概念，这意味着数据科学家可以取得渐进的进展，不要假设利益相关者需要最复杂的可用解决方案。

![](img/2cf8d3efd642bd3dc0b910099dadccde.png)

产生 MVA 的过程非常简单:(1)清楚地理解手头的业务问题，(2)产生快速和肤浅的见解来解决问题，(3)将结果反馈给利益相关者并获得他们的想法，以及(4)总结分析或深入挖掘。

通过记住这个框架，我能够为我当时工作的数据故事/技术报告/博客文章做出许多不同的迭代。在我的案例中，利益相关者是团队中的其他数据科学家以及不同职能部门的几位高管。

## **认知多样性**

我非常幸运能够与来自多个职能部门的同事交流，包括数据科学、营销/设计、法律、商业分析、产品管理和软件工程。这让我能够利用我所谓的**认知多样性**——观点或信息处理风格的差异。换句话说，它是个人如何思考和处理新的、不确定的和复杂的情况。

![](img/80c35329819e9b3917bd30556e8ca835.png)

给定一个实现机器学习模型来确定贷款/信贷申请人是被拒绝还是被批准的假设示例，这里有几个心智模型来解决这个问题:

*   数据科学家关心的是如何设计完美的实验来实现最佳性能的模型。
*   软件工程师关心如何建立合适的基础设施来将模型投入生产。
*   营销人员关心的是如何向公众传达模特使用的独特功能。
*   法律顾问关心如何解决与模型结果相关的潜在风险和合规性。
*   业务分析师关心如何计算模型对客户的业务影响。
*   产品经理非常关心上面提到的所有事情。

如果有一个收获是我真正感激的，那就是我能够开发的大量心智模型。通过学习倾听不同的意见，并以同事理解的方式用他们的语言说话/写作，我磨练了多侧面思考的能力——通过不太明显的推理，使用间接和创造性的方法解决问题的能力。

## **领域知识**

在 ZestFinance 实习之前，我对信用担保几乎一无所知。但是夏天过后，我对这个古老的行业有了更多的了解:

*   大约 2600 万美国人被联邦消费者金融保护局认为是“信用隐形人”,因为他们在三个信用机构中没有任何记录。另外 1900 万人没有足够的档案数据被贷款系统认为是可计分的。数以百万计的人在他们的信用档案的某个阶段有严重的错误被纠正。这 4500 多万美国人面临着真正的后果:更高的拒绝率、更高的贷款费用、劣质的金融产品——尽管其中许多产品实际上可能具有很高的信誉。
*   信用评分是 20 世纪最大的经济催化剂之一，但它已经跟不上今天的消费者了。可用于更准确和公平地对人评分的数据源的激增不能被传统的评分技术轻易或容易地消耗。
*   贷款人开始转向人工智能和机器学习承销，这些技术通过复杂的算法处理更多数据，可以处理杂乱或有缺陷的数据。机器学习信用模型从数百万次交互中得出结论，并使用比传统技术多 10 至 100 倍的变量。使用机器学习的银行和贷款机构报告了更高的批准率或更低的违约率，有时两者兼而有之，这是通过找到传统技术遗漏的好借款人(并拒绝可能已经获得批准的坏借款人)。
*   新的机器学习评分算法的制造商必须确保他们的模型不会延续当前贷款系统中存在的偏见。事实上，ZestFinance 的 ZAML 工具可以“去偏向”信贷和其他受监管行业的模型。

![](img/d0b368f7eaa594d878da8d819d3326a5.png)

在实习过程中，我获得了大量的领域知识，包括银行和金融机构如何对信贷申请人做出决策，他们如何采用机器学习，如何在模型设计中建立可解释性和公平性，以及如何确保模型的预测性能与其对企业客户的 ROI 值之间的相关性。

最重要的是，我真的很喜欢 ZestFinance 的使命驱动型文化，即建立一个让更多人获得信贷机会的世界。我对这家公司只有温暖的感觉，强烈建议你看看他们的[博客](https://www.zestfinance.com/blog)和[空缺](https://www.zestfinance.com/careers)寻找新的内容和工作机会。

## **收尾**

实习肯定重申了我对人工智能/机器学习的热情，我很感激我的工作确实为未来的工作留下了一些动力。快速分析和迭代实验阶段，与不同的利益相关者交谈所需的沟通技巧，解决各种商业领域问题的巨大潜在应用，都促成了我对这一领域的兴趣。

![](img/6ab210fb4fdd1df3bfd50846ff98ba91.png)

Me and fellow interns at the Wisdom Tree on top of Hollywood!

我非常感激有机会在这个夏天利用数据新闻为一个新兴行业的不可思议的产品创造价值。我完成了很多，犯了很多错误，最重要的是，由于一个令人敬畏的团队和一群多元化的导师，我学到了比我预期更多的东西。我希望我至少成功地向你们传达了一些教训。感谢您的阅读。

如果你喜欢这个作品，你可以在 https://jameskle.com/的[](https://jameskle.com/)**找到更多我的作品和项目。你也可以在*[*Twitter*](https://twitter.com/@james_aka_yale)*上关注我，在*[*GitHub*](https://github.com/khanhnamle1994)*，* [*上查看我的代码，直接发邮件给我*](mailto:khanhle.1013@gmail.com) *或* [*在 LinkedIn*](http://www.linkedin.com/in/khanhnamle94) *上找我。* [*注册我的简讯*](http://eepurl.com/deWjzb) *就在你的收件箱里接收我关于数据科学、机器学习和人工智能的最新想法吧！**