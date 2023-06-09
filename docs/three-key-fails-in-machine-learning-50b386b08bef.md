# 机器学习中的三个关键失败

> 原文：<https://towardsdatascience.com/three-key-fails-in-machine-learning-50b386b08bef?source=collection_archive---------23----------------------->

## 与机器学习相关联的神话可能会导致对何时以及如何应用机器学习的糟糕判断

我对分析学的介绍有点落后。我第一次大量参与任何类型的专门分析项目是机器学习项目。我的意思是，如果你要做这件事，为什么不做到底呢？

我不是在抱怨。这是一次奇妙的学习经历。它教会了我很多关于高级分析的技术方法。我了解了技术和数据管理。但最重要的是，我了解了一个神话是如何围绕着术语*机器学习*发展起来的，而事实上，它一点也不神秘。我记得在团队会议上，不知情的参与者将我们正在做的事情描述为“黑暗艺术”。

现实是，机器学习没有任何黑暗、神秘或神话的东西。在机器学习方法中采用的大多数统计方法在贝叶斯方法的情况下已经知道了几十年，甚至几个世纪。机器学习这个术语的激增完全是关于技术，以及它如何使我们能够以计算资源以前变得具有挑战性或完全不可能的方式将这些方法应用于大型数据集。

然而，神话依然存在。有很多人相信，或者被引导相信，机器学习项目可以执行某种超现代的魔法，挑战人类解决同一问题的所有方法。这是危险的，因为这可能意味着个人或团队在没有适当的批判性思维和人类判断的情况下，基于某种奇迹将会发生的信念，开始了占用大量资源和时间的努力。

在我继续之前，我想澄清一下:我不是在批评机器学习*本身*。有无数的使用案例表明，它带来了价值和效率，如果没有机器学习带来的突破，我们今天的生活将不会一样。不，我的观点是，我们不应该相信机器学习在所有情况下都有效，我们应该对如何以及何时投资这些技术更加谨慎。

为了说明我的观点，这里是我在机器学习项目中目睹的三个主要失败。

![](img/3ecb4b66509320b10de0c2eb4bc91e26.png)

# 1.目标设定不当

根据[我最近写的另一篇文章](/building-a-model-heres-the-first-question-you-should-ask-828befec5ac)，了解并阐明机器学习项目的目的是至关重要的。要么你建立你的模型来*解释*某事，要么你建立它来*预测*某事。大多数时候，一个更好地解释一种现象的模型在预测它时并不是最优的。此外，能够很好地预测某些事情的模型通常具有非常明显的特征，并且构成了预测能力的很大一部分，所以这并没有给它们很大的解释能力。

机器学习工作的目的得到所有各方的澄清和同意是至关重要的。我们建立一个模型主要是为了解释或预测。它不能两者兼而有之。这一点应该没有疑问。

![](img/1815557b40031af335e58bd4dcf12292.png)

# 2.糟糕的实验设计

假设你在一家销售公司工作，你想建立一个模型来解释是什么推动了销售代表的成功销售。你已经知道并且永远知道的一件事是，销售代表对现有客户的销售比对新客户的销售更成功。

你收集所有你能找到的数据，进行学习，然后在一次大型会议上宣布销售的三大解释性驱动因素是:

*   客户以前是否购买过
*   这是否是该代表以前拜访过的客户
*   在反馈调查中，客户是否对销售代表评价很高

显而易见，所有这些驱动因素都与一个我们已经知道很重要的因素有关，因此这种努力没有提供任何附加值，事实上，通过包括这些数据，模型的数学现在被一个我们已经知道的因素所主导。如果有人预先考虑如何设计工作，这是可以避免的。也许我们可以删除这些数据，或者将样本限制在该组之外的客户。

# 3.糟糕的实际规划

无论你是出于解释还是预测的目的开始从事 ML，很少有人会想到成功的后果。

如果你建立了一个可以帮助诊断员工缺勤原因的模型，或者一个可以预测生产问题的模型，或者其他什么模型，你需要能够实际部署它。这时，您会发现模型中使用的一些数据源是从需要大量手动操作的文件中提取的。或者您发现一些输入是基于缺失数据估算的。

关键是，如果您正在开发 ML，希望它在未来得到部署，以帮助更有效地诊断或预测事物，您需要确保输入数据可以轻松地流入预测引擎。我见过如此多的人工智能成果，它们使用的数据没有机会被轻易改造，这就产生了一个全新的令人头痛的问题，而这个问题本可以被更好地预测。

虽然机器学习为我们如何理解数据提供了如此多的潜力，但我们仍然远远没有达到任何数据集都能保证成功学习的地步。事实上，没有强大的设计和规划，没有对数据结构的良好直觉，机器学习项目最终可能会浪费大量的时间和精力。通过检查目标、实验设计和实际计划，你会很好地意识到它是否值得。

最初我是一名纯粹的数学家，后来我成为了一名心理计量学家和数据科学家。我热衷于将所有这些学科的严谨性应用到复杂的人的问题上。我也是一个编码极客和日本 RPG 的超级粉丝。在 [*LinkedIn*](https://www.linkedin.com/in/keith-mcnulty/) *或*[*Twitter*](https://twitter.com/dr_keithmcnulty)*上找我。*