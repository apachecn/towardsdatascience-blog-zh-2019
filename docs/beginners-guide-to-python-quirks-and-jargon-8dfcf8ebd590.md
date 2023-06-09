# Python 及其怪癖初学者指南

> 原文：<https://towardsdatascience.com/beginners-guide-to-python-quirks-and-jargon-8dfcf8ebd590?source=collection_archive---------19----------------------->

![](img/810058a93097118f26c91f8ceef0146f.png)

数据科学的繁荣欢迎了来自各行各业的大量新 Python 开发人员:从经验丰富的黑客、统计学家和数学家，到企业高管、记者，以及基本上任何想成为不可避免的数据革命一部分的人。各位，我们正处于激动人心的时代。我们正处于第四次工业革命的风口浪尖，每个人都想加入。

对于初学编程的人来说，Python 是数据科学的两种著名编程语言之一[，这非常方便。凭借其简洁的语法、易读性以及对自然语言的接近，难怪美国大学中 70%的编程入门课程都在讲授 i](https://dzone.com/articles/r-or-python-data-scientists-delight) t。我想不出比这更温和的编程入门了。

你可以选择所有的在线课程，所有的博客文章和教程遍布网络，学习语言的资源是不短缺的。此外，感谢像 [stackoverflow](http://stackoverflow.com) 这样的网站，如果你有任何问题，总会有一个其他程序员的社区来帮助你(大多数时候，我们大多数人都很好)。

获取知识从未如此简单，我想邀请你们所有人和我一起欣赏这一刻。

但是，虽然这些课程和教程可以让您快速掌握该语言和相关数据科学库的基础知识——仅举几个例子，pandas、numpy、matplotlib 和 sk learn——但大多数课程和教程几乎没有触及 Python 的复杂性。尽管 Python 很简单，但它是一门庞大而丰富的语言，了解它的内部和外部是值得的。

# 为什么它很重要

你可能只需要了解基础知识和足够的语言知识，就能在你的领域中发挥作用，但是了解你正在使用的语言的特点也有好处:

*   你可以写出更好、更有创意的代码。编程的核心是解决问题。掌握更多的语言知识可以让你考虑一个问题的多种解决方案。
*   你有可能加快工作速度。对于小型数据集，您可能不会遇到性能问题。当您开始处理至少几千行时，事情会变得更加冒险和不可原谅。知道哪种语言结构比其他语言结构工作得更快，可以将一个必须运行 34 小时的脚本转换成一个只需要运行 1 分钟的脚本(我很快会写这方面的内容！).
*   你未来的自己会感谢你。有没有做过六个月都没碰过的代码？没有吗？让我现在就告诉你:这不是一次愉快的经历。您不再是六个月前的问题领域专家。编写干净和一致的代码，即[python 化](https://hub.packtpub.com/write-python-code-or-pythonic-code/)的代码，将引导你养成按照某种风格模式编写的习惯，从而产生可读和可预测的代码。这肯定会节省你拉头发的时间。
*   **最后**，**为自己的工作感到骄傲**。好吧，这是我个人的想法，但我还是想分享一下。时间是非常宝贵的资源。如果你打算用它来创造一些东西，不妨创造一些让你自豪的东西。对我来说，在这种情况下，就是将我编写的代码与语言的设计方式结合起来。虽然编程通常被包装为逻辑问题解决，但在设计层面，它更像是艺术而非工程。这是你的创造力可以大放异彩的地方。

# **你应该知道的事情**

学习这些简单的概念，你将很容易成为一名更好的 Python 开发人员:

**空序列为假，有元素的序列为真。在条件句中使用时，不必知道列表、字典或集合的长度:**

Sequence Truthiness

**使用 enumerate()遍历序列。冒着听起来像个老人的风险，过去遍历一个列表和它的索引需要一组`len()`和`range()`。`enumerate()`让事情变得更简单:**

len() and range() vs. enumerate()

**你可以从字符串中创建列表。假设您想要创建一个由字母表示的类别列表，将它们制作成一个`string`并将其传递给`list`构造函数比手工制作更容易:**

Strings as Lists

**元组打包，序列解包。当你发现自己需要将多个项目组合在一起或从序列中提取单个项目时，可以使用这些工具。这些分别被称为元组打包和序列解包。**

Tuple Packing and Sequence Unpacking

通过利用打包和解包，可以在两个变量之间交换值:

Swapping Values

小心使用这个。虽然它增加了`x`和`y`之间的语义关系，但它也可能在两个非常不相关的变量之间提供错误的语义关系。

**F 弦**。从 Python 3.6 开始，您可以使用 f 字符串轻松地在字符串中加入任意表达式。对于旧版本 Python 的用户，有一个简单的解决方案:升级！如果这不是一个选项，您可以使用`string.format()`方法:

F-strings

f 字符串计算括号内的表达式，并自动将它们包含在字符串中。format 方法用传递给它的参数依次替换字符串中的花括号。如你所见，f 弦更加简洁。

***args，**kwargs。** `*args`和`**kwargs`允许函数接受任意数量的位置和关键字参数。当您事先不知道函数将要接收的参数数量时，这可能会很有用。在函数内部，`*args`可以作为列表访问，`**kwargs`可以作为字典访问:

*args and **kwargs

虽然在你的日常编程中找不到，但是当你在野外遇到它们时，这些知识是有用的。

**列表理解。**列表和理解允许你从现有的列表和字典中创建新的列表和字典。它们提供了简洁的语法，优于 for 循环。例子将有助于说明这一点。

假设您想要将列表中的所有值加倍:

Doubling Values in List Using Comprehension

或者可能在列表中找到奇怪的值:

Odds in a List using Comprehensions

列表理解提供了以下好处:

*   可读性增强
*   较少的代码行
*   潜在的性能提升(追加到数组会在运行时调整其大小，这会带来性能开销)

我可以保证你已经是一个更好的 Python 开发者了。

好吧，就这么定了。虽然我还想谈论更多的事情，但我想尽可能保持这篇文章的简洁，同时为读者提供直接相关的信息。毕竟我们都很忙。

实践这些，将它们整合到你的日常代码中，并进行实验。我向你保证，你的 Python 技能将会提高，你将能够编写出令你自豪的代码。

## 进一步阅读

关于 Python，还有很多东西需要学习，包括我提到的和我没有提到的。如果你想探索更多，我推荐以下这些文章:

*   [更深入的讲解列表理解](/comprehending-the-concept-of-comprehensions-in-python-c9dafce5111)。这里有大量清晰实用的例子。
*   [生成器，生成器函数，迭代器](/python-pro-tip-use-itertools-generators-and-generator-expressions-1b84911c978)。生成器通过使用[惰性评估](https://en.wikipedia.org/wiki/Lazy_evaluation)来帮助改善内存处理和性能。
*   [官方 Python 教程](https://docs.python.org/3/tutorial/index.html)。虽然有点枯燥，但我推荐任何认真的 Python 程序员阅读一下。它提供了理解语言的基本信息。

*Python 爱好者、艺术大师和老手们，你们能给那些刚刚加入这个行列的人提供一些技巧吗？下面评论下来！*

# 关于阿德里安·佩雷亚

*兼职数据科学家，兼职科技作家，全职书呆子。我在教授机器学习和可管理的、* ***字节*** *大小的程序中找到了乐趣。是的，我也很搞笑。咖啡上瘾者。数据可视化的吸盘。愿意为下一个最好的树状图付出我的 1 和 0。*

*关注我上*[*Twitter*](https://twitter.com/adrianmarkperea)*和*[*LinkedIn*](https://www.linkedin.com/in/adrian-perea/)*。*