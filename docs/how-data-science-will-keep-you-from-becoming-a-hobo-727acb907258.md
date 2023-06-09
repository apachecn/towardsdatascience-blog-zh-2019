# 数据科学如何让你不成为流浪汉

> 原文：<https://towardsdatascience.com/how-data-science-will-keep-you-from-becoming-a-hobo-727acb907258?source=collection_archive---------19----------------------->

## 蒙特卡洛的神奇一瞥

![](img/ab1aea649eb7976c301690a40174751d.png)

Source: Chicago Tribune historical photo

让我们从一些华而不实的高影响力统计数据开始。根据查尔斯·施瓦布 2018 年的现代财富指数，只有 1/4 的美国人有书面的财务计划，在没有的人中，只有 17%的人对实现他们的财务目标感到满意。

这是 62%的美国人不确定他们退休后会不会住在桥下吃猫粮，如果他们曾经住在桥下的话。谁也不能保证那 17%自信的人不会成为无业游民。

那么，我们如何才能让这些人享受到财务安全的舒适呢？我们如何让他们知道一切都会好起来的，或者有办法摆脱他们目前的处境？这两个问题的答案都可以通过制定一个全面的财务计划来找到，而今天的技术已经使得结合现代数据科学和数学方法来快速准确地揭示他们的财务未来成为可能。

财务计划是什么样的？我们如何把一个放在一起？一个真正好的财务计划会考虑到你现有的资产，你当前和未来的收入来源，比如社会保障，将它们与你当前和未来的支出进行对比，并为你的剩余资产附加一个增长率。

不幸的是，传统的财务计划看起来有点像这样:

![](img/2ca1c31abb074239f5382e9fa9b17a35.png)

So, so super successful

我认为我们都能看到这里的问题，我们在绝对地工作，而市场不是这样工作的。诚然，这是一个非常简化的版本，但它离真相不远了。财务顾问在介绍这一传统计划时，将回报率称为“目标”或“平均”回报率，他们将通过巧妙管理你的资金来实现这一回报率。有人可能会带着这样的印象离开这个会议，在 17 年后，他们会很高兴地坐在 120 万美元上，这是有保证的。毕竟，计划是这么说的，对吧？

但是，如果股市出现大规模崩盘，就像大衰退期间发生的那样，该怎么办？我们得调整模型，打印出来。如果你不得不拿出 20，000 美元上大学会怎么样？再次调整模型，打印出来。如果理财顾问不称职，年度回报到处都是怎么办？再次调整模型，打印出来。当你问完问题的时候，你已经带着 300 页的潜在假设，而你仍然没有对生活中一个重大问题的明确答案:**我能安全地退休吗？**

## 蒙特卡罗方法

![](img/ece01749b07db4e5beb1466a6eab5739.png)

Black line indicates actual path of Hurricane Sandy. Source: National Oceanic and Atmospheric Administration (NOAA)

我们无法准确预测未来，但我们可以确定不是 6%。当处理未知变量时，我们没有绝对，所以我们只能处理概率。让我们考虑一下天气，它每天每秒都在变化(除非你住在圣地亚哥)。如果气象学家对当前状况有足够的了解，他们可以在合理的误差范围内估计天气可能会是什么样子。他们使用蒙特卡洛建模来解释那些太不可预测的条件，并从那里可以确定他们每天的天气预报，甚至搜索潜在的飓风的天气情况。

蒙特卡洛建模，也称为蒙特卡洛方法或模拟，简而言之，是一种算法或过程，它使用随机性和概率来解决我们无法知道答案的问题，但希望通过产生高度概率的结果来尽可能接近问题。通过提供已知的数据，并随机化我们没有的变量，我们可以测试它数千次，以确定什么是最有可能的结果。这是一个在科学、数学和**数据科学、**领域使用的流行工具，我们将通过它来回答这个非常重要的问题。

它是怎么做到的？财务规划中最常见的方法是收集我们之前提到的传统变量，作为创建可靠财务计划的必要组成部分。然后，它绘制出第一年的图表，获取所有数据，并在给定的[标准差](https://simple.wikipedia.org/wiki/Standard_deviation)内选择一个随机回报率。这个标准差通常是根据客户投资组合的特征预先确定的。然后，该模拟基于该回报率调整客户当年的投资组合，并基于客户当年陈述的支出目标和/或储蓄增加或减少美元。接下来的一年，一年，一年，再一年都是如此，直到钱用完，或者模拟在预先设定的年份结束。然后再做**那个**全过程，一个**千遍**。最终，您会得到如下结果:

![](img/fa8b87ecc11fafa106b7be435d024e44.png)

The “broom” or “spaghetti” graph as we call it in “the biz” . Source: MoneyGuide Pro

看起来像飓风预报不是吗？你在上面看到的每一条灰线都是一次蒙特卡洛试验，或者说是一个客户的模拟财务寿命。正如你在这个例子中看到的，大多数线成功地到达了图的末端，只有少数线在到达终点线之前崩溃和燃烧。每一行对于我们试图回答的问题来说都是无关紧要的，但是结合起来，它们给了我们想要的真实结果。你在图表旁边看到的 88%告诉我们，在 1000 次试验中，有 880 次成功地带着至少 1 美元通过了终点线。现在，不是 300 页的“如果”,而是 1000 个“如果”,全部完全随机，包含了巨大和可怕的可能性，但都在一页上，结果被浓缩成一个结果:**迹象指向是** *(当然有很高的可能性)*。

然而，这个工具不仅仅是一个超级神奇的 8 号球，它还可以产生结果，你可以用它来分析和做出明智的决定。通过改变储蓄、支出或回报率等变量，您可以重新运行这些模拟以获得更优的结果。改变足够多的事情，你就已经建立了逃离流浪的框架。

这难道不令人兴奋吗？我们有真正的工作水晶球！我们应该把它用在任何事情上，这样就不会再有什么不好的事情了！不幸的是，坏消息来了。

## 蒙特卡洛的局限性

尽管蒙特卡洛令人惊叹，但它也有缺点。因为我们使用概率来运行每个试验，并且应用相同的概率范围，所以我们会遇到异常值的问题。看看下图中橙色圆点:

![](img/de67f84f9dd668439f5317fd437e0155.png)

“I want that one” — every client ever. Source: MoneyGuide Pro

这是一个失控的模拟，一个异常值。在我们客户的模拟生活中的某个地方，它在 [x 轴](https://study.com/academy/lesson/x-axis-definition-lesson-quiz.html)上急转弯，并从那里继续前进。惊人的回报叠加在更惊人的回报之上，再加上不断增长的余额。一旦它走得足够远，沿着我们的潜在回报分布，再多的左转都不会把它带回现实。以同样的标准来衡量，这些模拟中的每一个都有可能在两个方向上成为疯狂的局外人。这就像连续 10 次在轮盘赌桌上敲同样的数字。

那么这告诉我们什么呢？橙点先生告诉我们蒙特卡洛斯只能在一个非常固定的范围内工作。如果我们让它走得太远，随机绘图将变得更加极端，并产生级联结果，这将变得完全无用。在现实世界中，这意味着如果不对非常年轻的人进行一些调整，我们就不能可靠地使用它。可靠的蒙特卡洛模拟的理想范围是 40-50 岁左右，所以假设你活到 81 岁，社会保障精算表认为你会死*(用一堆盐来代替)*，你应该在 50 岁时开始认真对待这个问题，同时你还保留着**做出**改变的能力。当然，反过来也是正确的，蒙特卡洛模拟变得更加可靠*(可变性更小)*客户越老，但一旦退休，你就没有更多的方法从结果中得出结论。

另一个缺点是，随着股市的涨跌，我们使用的数据会不断变化，有时甚至以秒为单位。这意味着，我们刚刚运行的蒙特卡罗模拟只适用于我们运行它的那一秒。任何人都可以告诉你，你今天所做的决定取决于你在做决定时手头上的信息。我们不可能解释每一天每一秒都可能降临到一个人身上的近乎无限的可能性(“被公交车撞”的场景)。为了减轻这种情况，标准做法是定期重新审视和更新这一财务计划，通常是每季度或每年，但根据客户的情况，甚至可以低至每周一次。

不断变化的数据问题尤其与年轻客户相关，他们拥有几乎无限的金融潜力。一个年收入 10 万美元的 30 岁的人甚至还没有达到他们收入潜力的顶峰。他们还没有像他们的父母一样做出许多艰难的财务决定，比如生孩子，或者买房子，这使得他们未来成功的概率更难预测，因为没有足够的数据。虽然蒙特卡罗模拟可以让我们 30 岁的人模糊地看到他们的未来，但最好是将模拟隔离到更短期的目标，如为大学储蓄，或购买房子，同时关注未来。

## 阻止你流浪的未来

希望到现在为止，您已经对蒙特卡洛模拟有了更好的理解，并且能够帮助您制定出今天需要做的事情的框架。正确使用的话，这个工具可以帮助你做出明智的决定，这对你的未来有深远的影响，无论是经济上还是其他方面。不要等待，今天就开始计划，把这些技巧应用到你自己的生活中。

保护你自己和你爱的人不成为流浪汉。

在 LinkedIn 上与我联系！

[](https://www.linkedin.com/in/hamilton-chang-crpc%C2%AE/) [## 汉密尔顿·张，CRPC·CSPO-熨斗学校-纽约，纽约| LinkedIn

### 具有财务规划背景的数据科学家和机器学习工程师。我有专家级的知识…

www.linkedin.com](https://www.linkedin.com/in/hamilton-chang-crpc%C2%AE/)