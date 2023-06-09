# 在 Python 中使用 CSV、JSON 和 XML 的简单方法

> 原文：<https://towardsdatascience.com/the-easy-way-to-work-with-csv-json-and-xml-in-python-5056f9325ca9?source=collection_archive---------2----------------------->

![](img/4ecc90addea5b922c5ad567584d34c4f.png)

> 想获得灵感？快来加入我的 [**超级行情快讯**](https://www.superquotes.co/?utm_source=mediumtech&utm_medium=web&utm_campaign=sharing) 。😎

Python 卓越的灵活性和易用性使其成为最受欢迎的编程语言之一，尤其是对数据科学家而言。其中很大一部分是因为处理大型数据集是多么简单。

如今，每家科技公司都在构建数据战略。他们都意识到，拥有正确的数据:有洞察力的、干净的、尽可能多的数据，会给他们带来关键的竞争优势。数据如果得到有效利用，可以提供在其他任何地方都无法发现的深层洞察。

这些年来，可以用来存储数据的可能格式的列表显著增加。但是，有 3 种在日常使用中占主导地位:CSV、JSON 和 XML。在本文中，我将与您分享在 Python 中使用这 3 种流行数据格式的最简单方法！

# CSV 数据

CSV 文件是存储数据的最常见方式。你会发现大部分来自 Kaggle 比赛的数据都是这样存储的。我们可以使用内置的 Python csv 库读写 CSV。通常，我们会将数据读入一系列列表中。

查看下面的代码。当我们运行`csv.reader()`时，我们所有的 CSV 数据都变得可访问。`csvreader.next()`函数从 CSV 中读取一行；每次你调用它，它就移动到下一行。我们也可以像使用`for row in csvreader`一样使用 for 循环遍历 csv 的每一行。请确保每行中的列数相同，否则，在处理列表时可能会遇到一些错误。

用 Python 写 CSV 也一样简单。在单个列表中设置域名，在列表列表中设置数据。这一次我们将创建一个`writer()`对象，并使用它将我们的数据写入文件，与我们读取数据的方式非常相似。

当然，一旦你将数据读入一个变量，安装奇妙的 Pandas 库将使你的数据处理变得容易得多。从 CSV 文件中读取只是一行，将它写回文件也是一行！

我们甚至可以使用 Pandas 通过一个快速的命令行程序将 CSV 转换成字典列表。一旦您将数据格式化为字典列表，我们将使用`dicttoxml`库将其转换为 XML 格式。我们还会将它作为 JSON 保存到文件中！

# JSON 数据

JSON 提供了一种清晰易读的格式，因为它维护了一种字典式的结构。就像 CSV 一样，Python 有一个内置的 JSON 模块，让读写变得超级简单！当我们在 CSV 中阅读时，它会变成一本字典。然后我们把字典归档。

正如我们之前看到的，一旦我们有了数据，您可以通过 pandas 或使用内置的 Python CSV 模块轻松转换为 CSV。当转换成 XML 时，`dicttoxml`库总是我们的朋友。

# XML 数据

XML 与 CSV 和 JSON 有点不同。一般来说，CSV 和 JSON 由于简单而被广泛使用。作为一个人，它们读、写和解释起来既简单又快速。不需要额外的工作，解析 JSON 或 CSV 是非常轻量级的。

另一方面，XML 往往有点重。您正在发送更多的数据，这意味着您需要更多的带宽、更多的存储空间和更多的运行时间。但是 XML 确实比 JSON 和 CSV 多了一些特性:您可以使用名称空间来构建和共享标准结构、更好的继承表示，以及用 XML schema、DTD 等表示数据的行业标准化方法。

为了读入 XML 数据，我们将使用 Python 的内置 XML 模块和子模块 ElementTree。从那里，我们可以使用`xmltodict`库将 ElementTree 对象转换成一个字典。一旦我们有了字典，我们就可以像上面看到的那样转换成 CSV、JSON 或 Pandas 数据帧！

# 喜欢学习？

在[推特](https://twitter.com/GeorgeSeif94)上关注我，我会在那里发布所有最新最棒的人工智能、技术和科学！也在 [LinkedIn](https://www.linkedin.com/in/georgeseif/) 上和我联系吧！