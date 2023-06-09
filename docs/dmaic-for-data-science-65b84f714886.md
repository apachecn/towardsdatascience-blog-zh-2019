# DMAIC 数据科学奖

> 原文：<https://towardsdatascience.com/dmaic-for-data-science-65b84f714886?source=collection_archive---------20----------------------->

## 如何构建您的数据科学项目来创造商业价值

![](img/e67177fec9ee96d29f82c0d8ceb8544c.png)

View from Quandary Peak Summit

数据科学家的工作是分析数据以提取可操作的见解。

分析数据可能很容易，但是可操作的见解呢？虽然我们可以制作漂亮的图表和图形，这真的很酷，但我们如何才能真正证明它们提供了商业价值呢？

为了取得成功，我们必须学会将数据科学任务构建为一个业务问题，并定义我们如何增加价值。

当我被邀请为一个潜在的数据项目提供咨询时，我真的开始思考这个问题。我对他们正在做的事情感到兴奋，但我不确定如何将真正酷的想法变成可操作的产品，交付给最终用户。

在研究如何创建有价值的数据产品时，我发现了 DMAIC。

## DMAIC

我们可以使用数据驱动的问题解决方法 [DMAIC](https://en.wikipedia.org/wiki/DMAIC) 来思考我们如何使用数据来创造价值和改进流程。

DMAIC 是定义、测量、分析、改进和控制的首字母缩写。这是交付可持续和可量化成果的指导方针。

它是一个精确的数据科学发展过程吗？大概不会。但是我发现思考一下你什么时候想展示你的分析为什么有价值是很有帮助的。

## 规定

定义问题。

可以说，这是最重要的一步。如果我们能够在深入任何探索性分析、特性工程或建模之前预先定义问题，它将帮助我们看到真正的机会，并以有意义的方式将其框定。为了真正提供价值，从提高客户满意度的角度来考虑会有所帮助。

我们需要问自己一些重要的问题来为我们的项目建立最终目标和商业案例。这些问题对于确立焦点也很重要:我们需要能够创建一个可操作的产品并按时交付结果。

问题应包括:

*   有什么问题？
*   潜在的好处在哪里？
*   我们想要影响哪些指标？
*   我们计划如何影响这些指标？
*   是我们不关心的指标。
*   对一些指标产生负面影响可以吗？如果是，增加多少？

## 措施

测量当前基线。

这一步涉及到数据收集:从哪里获得数据以及我们需要多少数据是这里要考虑的要点。数据质量也很重要。

你将如何比较项目结束时和开始时的数据？

两个重点:缩短交付时间和提高质量。这里可能要问的问题包括:

*   我们当前的流程表现如何？
*   我们需要什么信息？
*   我们将如何收集数据？
*   哪些因素会影响我们的指标？

## 分析

分析数据。

最后是数据科学部分！在这一步中，我们可以调整正常的数据科学工作流程。

询问当前绩效与目标之间的差距。

*   我们如何改进目前的产品？
*   我们如何将数据可视化？

## 改善

改进项目并实施解决方案。

这是迭代步骤。我们如何改进当前流程来提高您的目标？我们如何更好地分析最后一步，以改进我们之前定义的指标？

在这一步中，我们还确定、测试和实施问题的解决方案。如果有明显的解决方法，就专注于它。不要过度复杂化！

## 控制

控制改进:让改变持续下去。

这是我们实施和监控产品的最后阶段。

记录您的流程。实施监控计划。

*   我们如何监控成功？
*   如果性能下降，我们该怎么办？

## 假设的例子

让我们通过一个假设的情况来看看我们如何使用 DMAIC 来确定我们作为数据科学家如何增加价值。

我们将基于过去的比赛场景: [Kaggle 的 Quora 不真诚问题分类](https://www.kaggle.com/c/quora-insincere-questions-classification/overview)并假设我们在 Quora 作为数据科学团队工作。

作为一个快速后台，Quora 是一个问答网站。有时人们会不怀好意地提问:试图激怒或冒犯其他用户。这显然是不好的，所以我们需要过滤掉那些不真诚的问题，不要让它们被张贴出来。

让我们想象一个假设和基本的当前流程:有一个分析师团队，他们手动审查每个问题。如果他们决定一个问题是真诚的，它将被发布到网上，否则它将被标记为不真诚，并被排除在网站之外。

这个过程听起来非常耗费人力、时间和效率。作为数据科学团队，我们建议创建一个机器学习模型来改善当前的流程。

在思考我们假设的问题时:

从高层次来说，Quora 问题的问题在于，有些人会问一些被认为有毒的问题。有毒的问题令人心烦意乱，令人不快。它们可能会导致服务使用率下降和客户满意度降低。因此，我们需要一个系统来标记和消除这些问题。

当前手动标记的解决方案可以工作，但是效率不高。由于我们是数据科学家，我们想利用机器学习创建一个新系统。

因此，我们**定义了**我们的主要目标:使用机器学习来识别和标记不真诚的问题。

我们假设当前基线涉及问题的手动标记。虽然这非常耗时且低效，但却有效且准确。

我们建议的解决方案需要更快，但也要保持当前手动方法的准确性。我们需要一种方法来**测量**的准确度。比赛使用了 F1 的分数，所以我们也可以用它作为我们的主要指标。我们还可以**测量**分析师的工作时间，以监控效率的提高。

接下来的步骤是**分析**和**改进**。在这里，我们将通过正常的数据科学流程来创建和改进一个模型，以过滤掉有害的问题。

最后，我们对我们的结果感到满意，因此我们实施了更改并进入了**控制**阶段。我们监控我们的解决方案并跟踪改进情况。

如果性能下降，我们可以计划回去重新分析新数据。所提问题的类型或措辞方式有变化吗？如果是这样，我们可能需要更新我们的模型。

## 结论

DMAIC 是增加我们数据科学工具箱的一个有用工具。

这对于从业务领导者和利益相关者关心的角度来构建数据科学问题，以及确保我们保持正轨并努力创建有用的数据产品非常有用。