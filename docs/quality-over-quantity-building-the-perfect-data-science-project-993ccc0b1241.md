# 质量胜于数量:构建完美的数据科学项目

> 原文：<https://towardsdatascience.com/quality-over-quantity-building-the-perfect-data-science-project-993ccc0b1241?source=collection_archive---------5----------------------->

![](img/f7fa73596953c5062acc310bba30e5e5.png)

credit: [https://www.housetohouse.com/diamonds-in-the-rough/](https://www.housetohouse.com/diamonds-in-the-rough/)

在初创公司的行话中，“虚荣指标”是公司为了让世界——有时是自己——相信他们比实际情况做得更好而跟踪的一个数字。

举一个突出的例子，大约八年前，Twitter 宣布[每天有 2 亿条推文通过其应用程序发送。这是一个很大的数字，但它并不像看起来那样相关:这些推文的很大一部分是由机器人发送的。此外，对 Twitter 作为一家公司的长期生存能力来说，真正重要的不是每天发送的推文数量；它是每日活跃用户的数量，以及在他们离开网站之前你可以向他们展示的广告数量。](https://techcrunch.com/2011/06/30/twitter-3200-million-tweets/?_ga=2.173065258.844637951.1547684180-1989064457.1535481657)

虚荣指标无处不在，当我们为它们优化时，它们真的会阻碍我们，而不是为重要的事情优化。他们让我们团团转，不明白为什么我们的努力没有结果。

现在，我在一家[数据科学导师创业公司](http://sharpestminds.com)工作。作为我工作的一部分，我审阅了许多由有抱负的数据科学家整理的 GitHub 投资组合。人们很难忽视一个特别的虚荣指标，许多人似乎以取得实际进展为代价来优化这个指标:*他们投资组合中数据科学项目的数量*。据我所见，很大一部分有抱负的数据科学家陷入了一个螺旋，即使用像`sklearn`和`pandas`这样的工具构建越来越多的数据科学项目，每个项目在过去的时间里都只有增量改进。

我想在这里探索的是打破这种恶性循环的方法，通过使用我们从看到几十个学员将他们的项目转化为工作面试并最终转化为工作机会中学到的一些关键经验。

所以，事不宜迟，以下是:一步一步地指导你建立一个伟大的数据科学项目，将带你超越 scikit-learn/pandas 螺旋，并让你尽快获得面试机会。

# 0.关键项目设计原则

在我们进入细节之前，这里有一些我们发现的一般原则，可以最大化一个项目转化为面试或工作的机会:

1.  你的项目应该是原创的。
2.  你的项目应该证明你有尽可能多的相关技能。
3.  你的项目应该表明你能做的不仅仅是处理数字。
4.  你的项目应该易于展示。

现在让我们看看这四个原则如何转化为具体的项目特性。

# 1.从哪里获取数据

![](img/06c2f9681a96c3e9460a6ea0f4466838.png)

决定要使用哪个数据集是设计项目时最关键的步骤之一。

当你这样做的时候，永远记住**原则 1** :你的项目应该是原创的。

以分析简历为生的技术主管和招聘人员每天会看到数百份简历，每份都有 3 到 4 个展示项目。你不希望你的简历成为他们今天看到的第 23 份分析泰坦尼克号生存数据集或 MNIST 的简历。作为一条规则，远离流行的数据集，甚至远离“训练轮”数据集，如 MNIST。正如我在之前[所讨论的，在简历中引用这些对你的伤害大于帮助。](/the-4-fastest-ways-not-to-get-hired-as-a-data-scientist-565b42bd011e)

另外要记住的是**原则 2** :你的项目应该展示尽可能多的相关技能。

除非你在一家大公司工作，在那里你的工作是高度专业化的，否则你将在工业中使用的数据很可能是肮脏的。非常脏。设计不良的模式，应该是`float`的`int`，T2 值，缺少条目，半缺少条目，缺少列名，等等。等。如果你想让雇主相信你具备在第一天就提高工作效率的所有技能，使用脏数据是一个很好的方法。出于这个原因，我一般建议避免 Kaggle 数据集(通常是预先清理过的)。

那么如果你也不能用 Kaggle 还剩下什么呢？网页抓取。很多很多。

使用像`beautifulsoup`或`scrapy`这样的库，从网上搜集你需要的数据。要么这样做，要么使用免费的 API 来构建一个别人没有的自定义数据集——并且您必须自己清理和争论。

是的，它比从 scikit-learn 导入虹膜数据集花费的时间更长。但这正是为什么很少有人这么做——也是为什么如果你这么做了，你更有可能被注意到。

# 2.使用 model.fit()之前要做什么

![](img/dd2030ee34e0961a2a14defc6387dfc9.png)

“训练轮”数据集通常有一两个明显的应用。

例如，泰坦尼克号数据集似乎提出了一个明确的分类问题:很难不想到，你可以做的最明显的事情是试图预测一个给定的人是否会在灾难中幸存。

但行业问题并不总是这样。通常，您会有一堆(肮脏的)数据，您需要弄清楚如何利用这些数据为您的公司创造价值。这就是**原则 3** 的用武之地:一个理想的项目不仅能证明你能够回答重要的数据科学问题，还能证明你能够提出这些问题。

一般来说，你如何提出好的问题来问？一个好的开始是做数据探索。

散点图、相关矩阵、维度缩减和可视化技术几乎都应该包含在这个步骤中。它们帮助你理解你收集的数据，以便你可以在进入项目的机器学习/预测阶段时想到好的问题，并通过为你提供易于在面试前和面试期间向面试官和招聘人员展示的情节，获得满足**原则 4** 的额外好处。

人们很容易忽视数据探索的重要性，但它确实是任何优秀数据科学项目中最关键的步骤之一。理想情况下，光是数据探索就能产生一两个令人惊讶的见解——这些见解将成为你在技术面试中讨论的绝佳素材。

# 3.主要结果

![](img/7ebc85b22fa01a0666541a9cdfc800d5.png)

credit: screenshot from [https://www.youtube.com/watch?v=BxizdTrItTk](https://www.youtube.com/watch?v=BxizdTrItTk)

当你决定你希望你的项目的主要产出是什么(即，你希望返回什么样的预测，或者你希望能够得出什么样的结论作为你的项目的主要结果)时，记住**原则 4** 是很重要的:不管产出是什么，如果它容易炫耀、好玩或者两者兼而有之，那是最好的。

出于这个原因，我建议将您的项目作为一个 web 应用程序向外界公开(使用 Flask 或其他一些基于 Python 的 web 开发框架)。理想情况下，你应该能够在聚会或面试中接近某人，让他们尝试几个输入参数，或摆弄几个旋钮，并向他们返回一些(理想情况下视觉上有吸引力的)结果。

将最终模型部署为 web 应用程序的另一个好处是，如果你还不知道 web 开发的基础知识，它会迫使你学习这些知识(如果你已经知道了，那么它会向雇主证明事实就是如此)。因为大多数面向产品的公司在他们产品的某一点上使用 web dev，如果有必要的话，理解服务器/客户机架构和基本的 web dev 可以帮助您更容易地将您的模型集成到生产环境中。

# 4.球场

一旦你建立了你的项目，你会想要开始向潜在的雇主推销它。这种推销应该不仅仅是在某人面前闪烁你的手机屏幕，告诉他们玩几个旋钮。

为了让你的项目更吸引人，确保你有一个关于你所做的事情的故事。理想情况下，这个故事应该包括你在数据探索或模型评估阶段获得的一两个意想不到的见解(例如，“事实证明，这个类很难与其他类区分开来，因为[原因]”)。

这对您有所帮助，因为它:

1.  围绕你的项目编一个更容易(也更有趣)让面试官记住的故事；和
2.  清楚地表明，你是一个重视弄清数据科学问题的人。

# 重复

当你向潜在雇主推销你的项目，并向其他数据科学家炫耀时，尽可能多地获得反馈，并迭代你的项目，以增加它的影响。

当你决定根据反馈对项目进行哪些改进时，优先考虑那些涉及学习新技能的事情，优先考虑那些当时最需要的技能。充分发展你的项目，而不是分散你的精力，最终你会拥有全面的技能。

但最重要的是，你会省去为虚荣指标盲目优化的时间，比如你已经完成的项目总数，所以你可以专注于唯一有价值的指标:被聘用。