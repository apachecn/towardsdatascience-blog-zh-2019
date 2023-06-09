# 如何在数据科学工作流程中使用测试驱动开发

> 原文：<https://towardsdatascience.com/tdd-datascience-689c98492fcc?source=collection_archive---------12----------------------->

![](img/445c18e9fb3f3605a5645a219e71afb1.png)

Photo by [Samuel Zeller](https://unsplash.com/@samuelzeller?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 数据科学家和机器学习工程师应该向软件开发人员学习的另一件事

每个软件开发人员都知道*测试驱动开发*(或简称 TDD)，但数据科学和机器学习方面的人不够多。这是令人惊讶的，因为 TDD 也可以大大提高数据科学项目的速度和质量。在这篇文章中，我将向您介绍 TDD 背后的主要思想和一个代码示例，该示例展示了 TDD 对于数据科学的价值以及如何在基于 Python 的项目中实际实现它。

# 什么是测试驱动开发？

TDD 是一种软件开发的进化方法。也就是说，它依赖于增量改进，这与敏捷过程相一致。

理解 TDD 最简单的方法是“红绿重构”——基于 Kent Beck 在 2003 年提出的工作模型的系统:

*   **红色:**编写一个新的测试，并确保它失败。如果通过，代码库已经覆盖了所需的功能，不需要额外的工作。
*   **绿色:**编写通过测试的代码。最重要的是，所有以前的测试也必须通过！也就是说，新代码增加了现有的功能。
*   **重构:**如有必要，修改代码。例如，确保代码库的结构在正确的抽象层次上。请勿在此阶段添加或更改任何功能。

您也可以将这些步骤视为寻找不同问题的答案:

*   如何检查我的代码是否提供了特定的功能？
*   绿色:我怎样才能写出通过我检查的代码？
*   **重构:**在不影响功能的情况下，我要在代码基上做什么改变才能改进它？

与其他方法相比，这种方法有许多优点:

*   编写测试迫使你思考用户以后可能会创建什么样的场景。一个好的测试涵盖了在给定特定输入或更一般的用户行为的情况下，软件应该交付什么。
*   你需要写更多的代码，但是每一部分都是经过设计测试的。整体质量将因此提高。
*   以这种范式思考促进了清晰定义的模块的开发，而不是过度复杂(并且难以维护)的代码库。

# 数据科学中何时(不)使用 TDD

希望我让你相信了 TDD 是软件开发的一个好主意。考虑到它的方法，我们什么时候可以在数据科学中应用这些原则以获得最大的效果？

**在以下场景中，TDD 可能不值得花费精力**:

*   你正在探索一个数据源，特别是如果你这样做是为了了解这个数据源的潜力和缺陷。
*   您正在构建一个简单明了的概念证明。你的目标是评估进一步的努力是否有希望。
*   您正在使用一个完整且可管理的数据源。
*   你是(并且你将会是)唯一一个在项目中工作的人。这种假设比乍看起来更强，但适用于特定分析。

相比之下， **TDD 在以下情况下更好**:

*   分析渠道
*   复杂的概念证明，即解决子问题的不同方法，干净的数据等…
*   处理数据的子集，因此您必须确保在出现新问题时，在不破坏工作代码的情况下捕获问题。
*   你在一个团队中工作，但是你想确保没有人破坏运行代码。

# TDD 示例:为 NLP 任务准备 Tweet

对于这个例子，我使用了标准 Python 库中的`pytest`而不是`unittest`。如果你在寻找后者的介绍，请看这篇文章底部的链接。

为了向您介绍 TDD 过程，我选择了一个简单但仍然现实的例子:准备一个 tweets 列表以供进一步分析。更具体地说，我想把分析建立在干净和独特的推特上。这需要针对四个子问题的代码:

1.  清除提及其他账户的推文。
2.  过滤掉转发。
3.  清除推文中的特殊字符。
4.  过滤掉空字符串。

我故意用一种后来并不理想的方式来排列它们。原因是:许多独立的测试可以涵盖这些任务中的每一项。这些任务的组合和顺序将在后面的单独步骤中进行。

因为我从一开始就知道这四个任务，所以我从为它们创建测试用例开始。也就是说，我想出了例证所有这些问题的典型推文。为了方便使用，我创建了一个`@pytest.fixture`函数。把这些函数想象成测试用例输入值的灵活占位符。以下是相关的代码片段:

我的所有代码都是一个更大的`tweet_project`模块的一部分，该模块包含一个`tweet_cleaning`文件，其中包含了与本例相关的所有函数。让我们从红色**开始这个过程:**

这个测试失败了，因为所有的`clean_mentions`函数现在包含的是一个`pass`。因此，它返回`None`而不是空字符串。现在是**变绿**的时候了，也就是编写通过测试的代码。在我的例子中，我使用了一个正则表达式来删除“@”和后面直到下一个空格的所有内容:

现在测试通过了。现在有什么可以对**进行重构的吗？没有直接影响功能的东西。**

我对其他三个步骤使用了相同的方法。以下是对他们的测试:

您可以看到`detect_`函数返回一个布尔值，该值可以在以后用作过滤器。我为通过这些测试而编写的相应函数如下所示:

这四个功能现在完全独立。他们每个人都有专门的测试，以确保他们按预期工作。为了结束这个例子，让我们构建一个测试来检查整个管道是否产生了期望的结果。也就是说，我想添加这样的功能:获取一组推文，清理需要清理的内容，过滤掉无用的内容，并返回一组推文以供进一步分析。

前面的测试用例没有充分涵盖潜在的场景。这就是为什么我为此实现了一个新的`pytest.ficture`。您还可以看到，我的测试涵盖了我想要的输出的两个基本特征。首先，它应该只从新的测试集中返回一条 tweet。其次，我需要确保结果是一个`list`,而不是一个集合或字符串(或者完全不同的东西),这样后面的函数就可以依赖它了。

红色的阶段是成功的，因为测试失败了。在**绿色**阶段，我使用了现有的(因此也是经过测试的)功能，并将它们组合起来，这样测试就通过了:

这段代码可以工作，但是对重构的需求是显而易见的。这既令人困惑，又有些丑陋。我鼓励你尝试练习。然而，无论你从现在开始做什么，所有的测试都必须保持绿色。在开始下一个周期之前，您不能添加额外的功能。

# 结论

我想强调的是，TDD 只能和程序员或数据科学家写的测试一样好。因此，思考哪些场景有可能发生是至关重要的。例如，在上面的例子中没有提到两次的测试用例。这里还有一些假设，比如数据中的转发总是以 rt 开头。

然而，这些并不是 TDD 的局限性，而是人类解决复杂问题的结果。TDD 的优势在于:

*   每个开发步骤本身都经过测试，很容易理解测试包含了什么。
*   因为每一步都建立在之前的测试之上，所以很难在不被注意的情况下破坏东西。这种方法大大减少了调试的需要。
*   对于如何向现有的代码库添加额外的功能，有一个清晰的方法:扩展现有的测试或者添加新的测试。
*   在 TDD 框架中工作鼓励明确的思考，并使其不太可能陷入死胡同或完全混乱。

我承认数据科学不同于软件开发。然而，时不时地像开发人员一样思考是一件很有力量的事情。

如果这篇文章对你有帮助或者你想补充什么，请在评论中或者在 [Twitter](https://twitter.com/TimoBohm) 上告诉我。我也很乐意在 [LinkedIn](https://www.linkedin.com/in/timo-boehm-datascience/) 上联系。**感谢阅读！**

## 附加材料:

关于使用 Python 中的`unittest`进行 TDD 的介绍，我推荐这篇由 [Dmitry Rastorguev](https://medium.com/u/6b041cd9ea98?source=post_page-----689c98492fcc--------------------------------) 撰写的博客文章:

[](https://medium.freecodecamp.org/learning-to-test-with-python-997ace2d8abe) [## Python 测试驱动开发的简单介绍

### 我是一个自学成才的初级开发人员，能够编写简单的应用程序。但我要坦白一件事。这是…

medium.freecodecamp.org](https://medium.freecodecamp.org/learning-to-test-with-python-997ace2d8abe)