# Python 的 5 个高级特性以及如何使用它们

> 原文：<https://towardsdatascience.com/5-advanced-features-of-python-and-how-to-use-them-73bffa373c84?source=collection_archive---------0----------------------->

![](img/8d34e5b6bea18f91ee6ba8a227ca76d2.png)

> 想获得灵感？快来加入我的 [**超级行情快讯**](https://www.superquotes.co/?utm_source=mediumtech&utm_medium=web&utm_campaign=sharing) 。😎

Python 是一门美丽的语言。简单易用，但表现力很强。但是，您是否使用了它所提供的一切？

任何编程语言的高级特性通常都是通过丰富的经验发现的。你正在编写一个复杂的项目，发现自己在 stackoverflow 上搜索一些东西。然后，您遇到了一个非常优雅的解决方案，它使用了一个您从来不知道存在的 Python 特性！

这是最有趣的学习方式:通过探索和意外发现！

以下是 Python 编程语言的 5 个最有用的高级特性——更重要的是如何使用它们！

# (1)λ函数

λ函数是一个小型的匿名函数——匿名是指它实际上没有名字。

Python 函数通常使用`def a_function_name()`的风格来定义，但是对于 lambda 函数，我们根本没有给它命名。我们这样做是因为 lambda 函数的目的是执行某种简单的**表达式或操作，而不需要完全定义函数。**

lambda 函数可以接受任意数量的参数，但必须始终只有一个表达式:

看那有多简单！我们执行了一些基本的数学运算，而不需要定义一个完整的函数。这是 Python 的众多特性之一，使它成为一种干净、简单的编程语言。

# (2)地图

Map() 是一个内置的 Python 函数，用于将函数应用于一系列元素，如列表或字典。这是执行这种操作的一种非常干净并且最重要的*可读的*方式。

看看上面的例子！我们可以将函数应用于单个列表或多个列表。事实上，您可以将地图与您能想到的任何 python 函数一起使用，只要它与您正在操作的序列元素兼容。

# (3)过滤

*过滤器*内置函数与*映射*函数非常相似，它将函数应用于序列(列表、元组、字典)。关键区别在于 *filter()* 将只返回应用函数返回为 *True* 的元素。

请看下面的例子以获得说明:

我们不仅评估了每个列表元素的真或假，而且 *filter()* 函数还确保只返回匹配为真的元素。非常方便地处理检查表达式和建立返回列表这两个步骤。

# (4)迭代工具

Python *Itertools* 模块是处理迭代器的工具集合。迭代器是一种可以在 for 循环中使用的数据类型，包括列表、元组和字典。

使用 *Itertools* 模块中的函数将允许您执行许多迭代器操作，这些操作通常需要多行函数和复杂的列表理解。下面的例子展示了 *Itertools 的神奇之处！*

# (5)发电机

*生成器*函数允许你声明一个行为类似迭代器的函数，即它可以在 for 循环中使用。这大大简化了您的代码，并且比简单的 for 循环更节省内存。

考虑一个例子，我们想把从 1 到 1000 的所有数字加起来。下面代码的第一部分说明了如何使用 for 循环来实现这一点。

如果列表很小，比如长度为 1000，这就很好了。当你想用一个巨大的列表，比如 10 亿个浮点数来做这件事时，问题就出现了。通过一个 for 循环，大量的内存咀嚼列表在内存中创建*—*不是每个人都有无限的 RAM 来存储这样的东西！Python 中的`range()`函数做同样的事情，它在内存中构建列表

代码的第(2)部分演示了使用 Python 生成器对数字列表求和。生成器将创建元素，并仅在需要时将它们存储在内存中*，即一次一个。这意味着，如果你必须创建 10 亿个浮点数，你只能在内存中一次存储一个！Python 中的`xrange()`函数使用生成器来构建列表。*

*这个故事的寓意是:如果你想要生成一个大范围的列表，使用生成器或者`xrange`函数。如果您有一个真正对内存敏感的系统，如移动或边缘计算，这一点尤其正确。*

*也就是说，如果你想多次迭代这个列表，并且它足够小，可以放入内存，那么使用 for 循环和`range` 函数会更好。这是因为生成器和`xrange`会在你每次访问它们的时候生成新的列表值，而`range`是一个静态列表，整数已经存在于内存中以供快速访问。*

# *喜欢学习？*

*在推特上关注我，我会在这里发布所有最新最棒的人工智能、技术和科学！也在 LinkedIn 上与我联系！*