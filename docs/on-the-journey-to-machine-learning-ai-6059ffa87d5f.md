# 在通往机器学习/人工智能的征途上。

> 原文：<https://towardsdatascience.com/on-the-journey-to-machine-learning-ai-6059ffa87d5f?source=collection_archive---------37----------------------->

## 让我们一起走过软件工程和机器学习之间的过渡之旅

![](img/eb9916ddb89607c0c7755c93c2210937.png)

这是我的第一篇关于机器学习(ML)的博客和我的旅程。从我作为一名软件工程师的职业生涯一开始，我就对所有与数据相关的东西非常感兴趣。

如果你对 ML 之旅中的一些小步骤感兴趣，它的基本原理以及你如何开始用它来构建项目，请跟我来，我会尽力解释我到目前为止学到的东西。

从我开始阅读和学习大数据、数据管道、数据科学、人工智能的那一刻起，我就知道未来将完全是关于数据的。

当然，当观察到我们(人类)是如何持续不断地产生大量数据时，我更加确信了，我忍不住要进一步挖掘我们如何、何时、何地利用这种新石油并从中获得最大收益。

***免责声明*** :这篇帖子的目的是分享我在学习和工作机器学习的同时所获得的知识。我将尽可能多地引用参考资料，如果您希望进一步扩展，也可以看看。

下面的帖子由 3 个部分组成，什么是机器学习，从软件工程的角度来看，它如何改变范式，以最终确定为什么每个人都对将其融入生活如此感兴趣或不感兴趣。

# **什么是机器学习？**

到处都有数百万个关于机器学习的定义，我将在这里指出我最喜欢的几个。

> 与人脑的类比被用作指导原则……调查主要围绕应用于机器的模拟教学过程。图灵，A. [智能机械，1948](https://storage.googleapis.com/laurau_blog/intelligent_machinery_turing.pdf) 。
> 
> 一个研究领域，它赋予计算机学习的能力，而无需显式编程。**阿瑟·塞缪尔，1959 年**

**我该如何定义？**

机器学习是一个科学领域，它可以帮助你以比我们人类在计算机的帮助下更快的速度发现模式。想象一下，就像将你所有的数学知识应用于数据，并应用技术，使得从你作为算法输入的数据中提取那些模式并得到答案成为可能。

# **随着 ML 的出现，编程范式如何转变？**

如果你是一名软件工程师，下面的解释可能会引起你的共鸣。

假设您正在构建一个智能手表应用程序，该应用程序将帮助您检测您在健身房进行的锻炼的类型，并且到目前为止，出于本示例的目的，您的应用程序仅检测您何时使用跑步机或踏步机。

太好了！您已经在应用程序的后端内置了一些规则来检测它是否正在使用这些机器并计算卡路里，如下所示:

但是，这里有一个问题:

*   一年后，当 5 台不同品牌的机器进入市场，智能手表的所有者开始使用其中一台您尚未添加的机器时，会发生什么？
*   当一家健身房的老板希望你将他所有的器械添加到你的应用程序中，并且他拥有许多品牌，大约有+20 台器械时，会发生什么情况？

除了这些新的限制之外，你还应该考虑做运动的人，体重，心率等等。

好吧，这看起来像是在应用程序中编码了很多规则。这种模式仍然在许多应用程序中使用，并且仍然适用于编程的常见用途，如下所述:

**传统编程范式**

规则和数据是输入，我们得到答案作为输出:)

**例如:**你今天在跑步机上跑了 15 分钟，消耗了 200 卡路里:)

*如果我告诉你，你可以把这个转过来，让电脑自己算出规则来*会怎么样

**新的编程模式**

数据和答案被输入算法，结果就是规则

**例**:你让算法知道有哪些功能可以使用:

*   机器 A(速度、速率、倾斜度)和它的值，然后你说:“这就是跑步机使用的样子”
*   机器 B(每分钟步数、速度、程序)及其值，你说:“这就是踏步机使用的样子”

诸如此类，你给算法提供了很多例子。因此，下次智能手表的主人使用新机器时，你的智能手表将能够**推断**正在使用腿压，并将自行计算一切。

这有多棒？能够输入数据，让计算机为你计算出规则，这样你就不必花几个小时的时间编写无限的规则；-)

现在，让我们进入文章的最后一部分，我将解释这是多么有用，为什么我们要实际使用它。

# **我们为什么要用机器学习？**

围绕智能机器有很多研究正在进行，我毫不怀疑我们可能会在某个时候生活在一个与这些机器分享我们日常生活的新时代。我们甚至可以说，随着智能辅助的出现，我们正在做这件事，我们日常使用的软件和应用程序中嵌入了推荐系统，如网飞、Airbnb、亚马逊等，但我仍然要说，还有很多事情要做，需要尝试。

如果你以前读过机器学习和人工智能，你可能知道围绕这个话题有很多争议，特别是与自动化、机器抢走我们的工作以及我们都因机器智能的崛起而被解雇有关。好吧，让我告诉你这与事实相去甚远。

在我看来，机器学习/人工智能应该被视为对我们技能的补充，对我们的优势和弱点的补充，最终作为一种工具，我们通过建立模型来帮助计算机，计算机帮助我们以我们无法达到的速度进行计算。

到目前为止，我在商业、社会和生活中看到的好处是巨大的，这里有几个例子:

*   从胸部 x 光检测肺炎的可能性，这是由[Stanford](https://stanfordmlgroup.github.io/projects/chexnet/)开发的深度学习算法
*   [农民伴侣应用](https://blog.google/technology/ai/machine-learning-meets-african-agriculture/)，这款应用有助于检测和识别作物何时被毛虫感染，并建议你如何处理以阻止其发生。

后者是一个很好的例子，说明我们实际上如何让机器学习成为我们生活和技能的一部分，以促进我们的工作，或许在我们的业务中用更少的资源生产更多的东西，或者只是为了生活在一个更好的世界。

如果你对周围有哪些类型的机器学习更感兴趣，以及如何开始思考是否值得将它应用到你的业务用例中，请留下来并关注我，因为我计划在接下来的帖子中写更多关于它的内容。