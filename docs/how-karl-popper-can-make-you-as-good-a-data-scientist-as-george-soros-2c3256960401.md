# 卡尔·波普尔如何让你成为像乔治·索罗斯一样优秀的数据科学家

> 原文：<https://towardsdatascience.com/how-karl-popper-can-make-you-as-good-a-data-scientist-as-george-soros-2c3256960401?source=collection_archive---------12----------------------->

## 数据科学之道

## 波普尔关于“可证伪性”和如何建立更好的机器学习模型的观点

[*数据科学之道*](https://medium.com/tag/the-tao-of-data-science) *专栏探讨了几个世纪以来哲学家们是如何攻克机器学习和数据科学的关键问题的。*

![](img/a0e649cc2bd15b15eebb1de1d4a8313a.png)

If Karl Popper were a modern data scientist, he would have used the concept of “falsifiability” when he implemented machine learning models.

卡尔·波普尔最著名的观点是科学通过“可证伪性”前进——这个观点认为一个人**不能**证明一个假设是真的，或者*甚至通过归纳*获得真理的证据(哎呀！)，但一个人可以反驳一个假设，如果它是假的。

# 如果波普尔是一名数据科学家…

假设 Popper 是一名现代数据科学家，需要实现一个机器学习解决方案来预测一些感兴趣的现象。考虑到他的科学哲学，他会如何实施他的模型呢？

**Popper 将实现一个因果模型**。因果机器学习模型直接对建模者旨在预测的现象中起作用的因果机制进行建模。对因果机制进行建模使得能够在对系统进行干预的情况下进行稳健的预测，即使这些干预导致系统的行为方式与它在训练数据中的行为方式根本不同。术语“干预”指的是任何人为的“搞乱”你正在建模的事物的方式。例如，在金融建模中，干预的一个例子可能是新的税收政策。如果你有一个模型可以预测你的电子商务平台的销售收入，那么开展广告活动就是一种干预。

Popper 将通过以下**迭代模型反驳**算法建立模型:

1.  基于如何改进您的模型的先前迭代的想法，您提出了一个更新的模型。
2.  你使用新的模型来预测干预的结果。在选择关注哪种干预措施时，优先选择预测结果更令人惊讶的干预措施。
3.  你实际上进行干预并观察结果。如果结果与预测不符——嘣！模型伪造。
4.  重复步骤 1–3。一直走下去，直到找不到方法去证伪 model 的当前迭代。

***你知道波普尔不会做什么吗？*** 他会**而不是**专注于优化某些函数的可能性或预测准确性。他知道模型平均来说可以预测得很好，但在重要的边缘情况下仍然预测得很差。

# 波普尔可能仍然是一个平庸的数据科学家

让我们面对现实吧，有时候你所需要的只是一个很好的预测。一个优秀的数据科学家能够识别何时是这种情况，何时不是。

然而，Popper 方法的另一个问题出现在步骤 1 中。在这一步中，Popper 必须从大量的候选模型中进行选择，这些模型尚未被之前迭代中的干预实验数据所证伪。

大多数数据科学家会根据来自所有这些先前实验的证据在多大程度上支持给定候选人来对候选模型进行排名，例如使用[交叉验证](https://en.wikipedia.org/wiki/Cross-validation_(statistics))，或者基于可能性的标准，如 [AIC](https://en.wikipedia.org/wiki/Akaike_information_criterion) 或 [BIC](https://en.wikipedia.org/wiki/Bayesian_information_criterion) 。

不是波普，他的口头禅是:

> “你无法证明一个假设(即模型)是真的，甚至无法通过归纳法证明它是真的，但如果它是假的，你可以反驳它。”

因为对波普尔来说，可证伪性才是最重要的，所以每一个候选模型都和其他模型处于同等地位。没有什么能帮助他喜欢一个模型。鉴于他必须搜索尚未被反驳的模型的巨大空间，这使他的算法的有效性受到质疑。

然而，我们不必像波普尔那样反对有证据的归纳推理。我们可以使用上面的模型构建算法，并为下一次迭代选择在前一次迭代中得到有力支持的模型。

# 波普尔如何让你成为像乔治·索罗斯一样优秀的数据科学家？

波普尔给我们的最有价值的想法是，通过设计可能失败的情况，尽最大努力打破你的模型，然后根据这些情况改进模型。

虽然你并不完全需要一个因果模型来做到这一点，但它肯定会使这个过程变得容易得多。如果没有预测干预效果的方法，就很难识别模型的故障模式。仅仅因为你不知道什么样的边缘案例破坏了你的模型，并不意味着一旦你的模型进入生产，这些边缘案例就不会出现。

金融投资是一个罕见的边缘案例可以毁掉你的领域。如果你认为财富是这种建模技术的证据，那么看看亿万富翁投资者乔治·索罗斯就知道了。早在“数据科学”出现之前，索罗斯就已经将数据科学应用于金融市场。

![](img/607f187240b177ccdcd15afff86ad1e7.png)

BIllionaire George Soros attributes his investment success to Popper’s philosophy

索罗斯也是波普尔在伦敦经济学院的学生，并称赞波普尔启发了他的“反身性通论”。这是因果理论——因果机制是宏观经济的抽象概念——是他投资策略的核心。他的策略可以总结为**之上的**迭代模型反驳**算法。**

> 我富有只是因为我知道什么时候我错了……我基本上是通过认识到自己的错误而生存下来的。乔治·索罗斯

如果对他有用，也许对你也有用。

**延伸阅读:**

*   卡尔·波普尔 —斯坦福哲学百科全书
*   [归纳问题](https://plato.stanford.edu/entries/induction-problem/) —斯坦福哲学百科全书
*   索罗斯乔治。"易错性、反身性和人类不确定性原理."*经济学方法论杂志*20.4(2013):309–329。