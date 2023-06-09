# 目标情感分析与传统情感分析

> 原文：<https://towardsdatascience.com/targeted-sentiment-analysis-vs-traditional-sentiment-analysis-4d9f2c12a476?source=collection_archive---------21----------------------->

## 想要找到一个句子对该句子中的实体的情感吗？那么情绪分析对你来说可能还不够……请继续阅读，了解有针对性的情绪分析！

![](img/e9878bc00ff611be0632b60da38e1200.png)

在某些情况下，我们可能不想从整个文本中提取情感，而是预测该文本对其中某个实体的情感。当这是我们的目标时，返回整个文本文档的整体情感的传统情感分析是不够的，我们需要开发一种更复杂的技术: ***有针对性的情感分析*** 。在这篇文章中，我们将解释它们之间的区别，并用一些简单的例子来说明这种不同的行为。

那我们走吧！

# 打住，我不知道什么是情绪分析！

别担心，一如既往，我在你身边。情感分析是一种自然语言处理(NLP)技术，其中给定某个文本文档作为输入，我们得到这样的文本的情感(积极的、消极的，有时是中性的)作为输出。在某些情况下，我们甚至可以获得一系列的情绪，如非常积极、适度积极、中性、适度消极和非常消极。

![](img/65a590347f5d6877798471d1751de865.png)

这些模型通常来自两个不同的家族: ***字典方法*** 和 ***机器学习方法。*** 前者利用具有正负极性的词典来推断文本是正的还是负的。这意味着寻找像*“好的”、“伟大的”、“惊人的”、“棒极了的”、“T15”或*“爱”*这样的词，以查看文本是否是积极的，或者像*“坏的”、“可怕的”、“可怕的”、“T19”或*“讨厌”*这样的词，以查看文本是否是消极的。**

后者使用大量先前被标记为正面或负面的文本文档，从数据中学习哪些模式形成正面或负面文档，然后通过寻找这些模式来预测新文档的情感。

情绪分析有很多真实的用例:它可以用于跟踪企业在一段时间内的客户情绪，推断产品的可能性，社交网络用户对某些话题的看法，甚至预测总统竞选或颁奖仪式等事件的结果。

让我们看一些使用[平行点在线情感分析工具](https://www.paralleldots.com/sentiment-analysis)的句子和情感分类的例子。

![](img/e3b246ee72b3c5eecb026ee832934e40.png)![](img/614629f506cda3ce4b572a6fa0e8bc59.png)![](img/8aec52dd15784ffddca1a6f7dc2454d4.png)

正如我们所看到的，对于每一句话，我们都得到了一个情感预测(正面的、中性的或负面的)以及对该预测的信心。置信度最高的情感是被挑选出来作为整个句子的潜在情感的情感。(如果你想知道，在写这篇文章的时候，我没有去过汉堡店，但是我很想去)

正如我们在这些例子中看到的，情感分析可以用来从一个句子中提取整体情感。然而，如果我们想要对文本文档中特定实体的情感，而不是整个文本的情感，会发生什么呢？考虑下面的句子:

****汉堡店*** *还不错，但我这一天过得相当糟糕:我被老板吼了一顿，我吃了一块以为是巧克力片但其实是恶心的葡萄干的饼干，我还在地铁上滑倒了**

*假设我们想知道说话者对汉堡店的看法。 如果我们使用与之前句子相同的在线传统情感分析工具，我们会得到以下结果:*

*![](img/76c8124b78b832ff7e817b949fa85055.png)*

*正如我们所看到的，因为该句子带有总体负面情绪，所以即使对汉堡店 的情绪是正面的，传统情绪分析的输出也是负面的。这是因为它不是分析对它的特定情感，而是分析整个句子的情感。*

*如果想要分析文本中对特定目标的情感，我们必须使用普通情感分析的变体，称为 ***目标情感分析。****

# *有针对性的情感分析:发现对…的情感*

*目标情感分析所做的基本上是获取文本和该文本中的给定实体，并预测文本中反映的对该实体的情感。在前面的情况下，给定相同的句子，并且将汉堡 ***地点*** 作为目标实体，有针对性的情感分析模型将试图预测说话者对汉堡地点的情感，而不是整个句子的实际情感。*

*作为定向情感分析模型，我使用了刘和张的双向模型，分别来自*、*、*、、*、*，其中*、*预测对*汉堡店*的正面情感，置信度在 80%以上。如果你不知道什么是 LSTM，你可以在我之前关于 NLP 的[深度学习](/deep-learning-for-nlp-anns-rnns-and-lstms-explained-95866c1db2e4)的帖子中找到。**

*好吧，这很酷，但是有针对性的情感分析实际上可以用来做什么呢？嗯，它可以执行许多与传统情感分析相同的任务，以及一些更复杂的任务。例如，我在一个项目中使用它来分析对 Twitter 社交网络上某个主题的最重要个人的情感。我分析了像英国退出欧盟或奥斯卡这样的话题，发现了 Twitter 用户对这些话题中某些有影响力的人物的总体看法。考虑以下推文:*

1.  **“我不得不说，奥斯卡颁奖典礼很无聊，糟糕的主持人，糟糕的评论，以及尖锐的提名，然而****@ lady Gaga****看起来如此令人惊讶 beutiful❤#奥斯卡奖”**
2.  *今晚我对#NewsNight 上的***@ mait lis****再尊重不过了，口头上把所有级别的 sht 赶出了每一个被采访的完全被欺骗的议员，因为他们触发了 A50 离开我们# 2 周，直到彻底的灾难。去你们的。#英国退出欧盟"**

*![](img/fbce8cef87a3e63cf340513be17c3e77.png)**![](img/4de80aa559323365f6aa9df4ec8705bb.png)*

*第一条推文使用传统的情感分析器，返回低置信度的负面标签，然而，如果使用有针对性的情感分析模型来分析对 ***@ladygaga*** 的情感，则返回超过 60%置信度的正面标签。第二条推文，当作为一个整体来分析时，具有非常强烈的整体负面感觉，然而，如果用有针对性的情感分析来分析对 ***@maitilis*** 的情感，我们再次获得正面标签，并且具有很高的可信度。这两个结果都与我们通过阅读推文所看到的相符。*

*在该项目中，我通过过滤不同的标签收集了大量关于每个主题的推文，找出了谁是被提及最多的用户(将他们定义为该主题中最有影响力的人物)，并通过使用有针对性的情感分析模型计算了网络用户对这些有影响力的人物的总情感，其中推文的文本和该文本中被提及的用户作为模型的输入目标。*

*这些方法对企业非常有用，允许他们超越传统情感分析的限制，从现有数据中探索新的见解。*

# *结论*

*在这篇文章中，我们看到了传统情感分析和有针对性的情感分析之间的差异，展示了它们可能被使用的不同场景。*

*在下一篇文章中，我们将探索不同的机器学习方法如何进行情感分析和有针对性的情感分析，深入探讨它们在特征和模型方面的差异。*

*非常感谢你的时间，不要担心，我不需要任何情绪分析就知道你看完这篇文章后很开心:)*

*如果你喜欢它，一定要在媒体、**和**上**关注我，也可以在 [LinkedIn](https://www.linkedin.com/in/jaime-zornoza/?source=post_page---------------------------) 上和我联系，或者在 Twitter @ jaimezorno 上关注我。另外，你可以看看我在数据科学和机器学习方面的其他帖子[这里](https://medium.com/@jaimezornoza?source=post_page---------------------------)。好好读书，保重！***

*![](img/65ac89452f70111d214827373dc1aafd.png)*