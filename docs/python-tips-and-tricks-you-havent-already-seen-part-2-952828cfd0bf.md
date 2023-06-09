# 您还没有看过的 Python 技巧和诀窍，第 2 部分

> 原文：<https://towardsdatascience.com/python-tips-and-tricks-you-havent-already-seen-part-2-952828cfd0bf?source=collection_archive---------16----------------------->

*注意:这最初发布在*[*martinheinz . dev*](https://martinheinz.dev/blog/4)

几周前，我发表了一篇文章([此处为](https://medium.com/@martin.heinz/python-tips-and-trick-you-havent-already-seen-937f14a08a08))关于一些不太为人所知的 Python 特性，很多人似乎都喜欢它，所以这里有另一轮 Python 特性，希望你还没有看到。

![](img/cb8e7f1fdfceb4fd60d10324cdb4773d.png)

# 使用`slice`功能命名切片

使用大量硬编码的索引值很快会导致维护和可读性方面的混乱。一种选择是对所有索引值使用常量，但我们可以做得更好:

在这个例子中，我们可以看到我们可以避免神秘的索引，首先使用`slice`函数命名它们，然后在切掉字符串的一部分时使用它们。您还可以使用切片对象的属性`.start`、`.stop`和`.step`来获得更多关于切片对象的信息。

许多命令行工具或脚本需要用户名和密码才能操作。因此，如果您碰巧编写了这样的程序，您可能会发现`getpass`模块很有用:

这个非常简单的包允许您提示用户输入密码，并通过提取当前用户的登录名来获取他们的用户名。请注意，不是每个系统都支持隐藏密码。Python 会试图警告你这一点，所以只需在命令行中阅读警告。

现在，对于 Python 标准库的一个更难理解的特性。如果您发现自己需要使用类似于[Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance)Python 和`difflib`的工具来查找类似于某个输入字符串的单词，您会得到支持。

`difflib.get_close_matches`找到最佳的*【足够好】*匹配。这里，第一个参数与第二个参数相匹配。我们还可以提供可选参数`n`，它指定要返回的最大匹配数。可以设置另一个可用的关键字参数`cutoff`(默认为 0.6)来改变匹配字符串得分的阈值。

如果你必须用 Python 做一些网络工作，你可能会发现`ipaddress`模块非常有用。一个用例是从 CIDR 生成 ip 地址列表(*无类域间路由*):

另一个很好的特性是 ip 地址的网络成员检查:

还有很多更有趣的特性我就不赘述了，因为你可以在这里找到那些。但是请注意，在`ipaddress`模块和其他网络相关模块之间只有有限的互操作性。例如，您不能使用`IPv4Network`的实例作为地址字符串——它们需要首先使用`str`进行转换。

如果你是一个拒绝使用 IDE 并且用 Vim 或 Emacs 编码的人，那么你可能会遇到这样一种情况，在 IDE 中使用调试器是很有用的。你知道吗？你有一个——用`python3.8 -i`运行你的程序——`-i`会在你的程序终止时启动交互式 shell，从那里你可以探索所有变量并调用函数。很好，但是*实际的*调试器(`pdb`)怎么样？

让我们使用下面的程序(`script.py`):

用`python3.8 -i script.py`运行脚本

我们看到了崩溃的位置，现在让我们设置一个断点:

现在再运行一次:

大多数情况下，打印语句和回溯对于调试来说已经足够了，但有时，您需要开始探索一下，以了解程序内部发生了什么。在这些情况下，您可以设置断点，当您运行程序时，执行将在断点处停止，您可以检查您的程序，例如，列出函数参数、计算表达式、列出变量或如上所示单步执行。`pdb`是全功能的 python shell，所以你可以执行任何文学上的东西，但是你需要一些调试器命令，你可以在这里找到

一个在编程语言中很常见，但在 Python 中不常见的特性是函数重载。即使不能重载普通函数，也可以使用类方法重载构造函数:

你可能会倾向于将备选构造函数的所有逻辑放到`__init__`中，并使用`*args`、`**kwargs`和一堆`if`语句来解决它，而不是使用类方法。这可能行得通，但可能会变得难以阅读和维护。因此，我建议在`__init__`中加入很少的逻辑，并在不同的方法/构造函数中执行所有的操作。通过这种方式，对于类的维护者和用户来说，你将得到干净清晰的代码。

您是否曾经编写过执行昂贵的 I/O 操作的函数，或者可以从缓存(内存化)结果中获益的相当慢的递归函数？如果你这样做了，那么使用来自`functools`的`lru_cache`有一个简单的解决方案:

在本例中，我们正在缓存 *GET* 请求(最多 32 个缓存结果)。您还可以看到，我们可以使用`cache_info`方法检查我们函数的缓存信息。装饰器还提供了一个使缓存结果无效的`clear_cache`方法。我还想指出，这不应该用于有副作用的函数或每次调用都会创建可变对象的函数。

在列表中找到最常见的项目是一项非常普通的任务，你可以使用`for`循环和字典(map)来完成，但这将是浪费时间，因为在`collections`模块中有`Counter`类:

在幕后，`Counter`只是一个将条目映射到出现次数的字典，因此您可以像使用普通的`dict`一样使用它:

除此之外，您还可以使用`update(more_words)`方法轻松地添加更多的元素到计数器中。`Counter`的另一个很酷的特性是，你可以使用数学运算(加法和减法)来组合和减去`Counter`的实例。

我认为，如果你正在使用 Python，这次我在这里分享的大多数技巧几乎每天都有用，所以我希望它们能派上用场。此外，如果你对这些 Python 技巧和诀窍有任何想法，或者如果你知道解决上述问题的任何更好的方法，请告诉我！🙂