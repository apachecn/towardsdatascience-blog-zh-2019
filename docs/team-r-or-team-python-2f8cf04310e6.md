# R 队还是 Python 队？

> 原文：<https://towardsdatascience.com/team-r-or-team-python-2f8cf04310e6?source=collection_archive---------8----------------------->

![](img/b1eb05a399e6298a5e4f165864977b3b.png)

“一个公认的事实是，一个在计算机科学和统计学方面有良好基础的数据科学家，肯定需要一种编程语言。”

嗯，我敢肯定，如果数据科学早在 1813 年*的《傲慢与偏见》第一次出版的时候，简·奥斯汀*就会*这样表达。*

随着点击统计和机器学习工具的存在，如 Weka、SPSS 和谷歌的 AutoML，人们很容易陷入这样一个陷阱，即认为在数据科学领域建立职业生涯时，能够编程不再重要。

虽然我不否认技术的发展变化，而且理解数据科学的理论比用代码实现它更重要。事实是，如果你想在数据科学领域有所成就，你需要会编程。

事实上，在我最近对 LinkedIn 上列出的 100 个数据科学职位广告进行的分析中，我发现 97%的广告都将编程技能作为选择标准。

能够编程给了你能够提取和争论你自己的数据的自由；让您更好地控制模型参数调整；这意味着当涉及到您能够使用的算法和技术范围时，您不再受软件开发人员的摆布。

但是有这么多编程语言可供选择(维基百科列出了几百种)，你应该从哪里开始呢？

在为数据科学选择编程语言时，需要考虑以下六点:

# #1:雇主想要什么编程语言？

如前所述，我最近检查了 2019 年 4 月 22 日至 2019 年 5 月 5 日期间在 [LinkedIn](https://www.linkedin.com/jobs/) 上发现的四个英语国家(澳大利亚、加拿大、英国和美国)的 100 份数据科学招聘广告。

这些招聘广告被选择来代表雇主类型、规模、行业和工作级别的广泛代表性，而纯粹的管理角色没有被考虑。

基于这一分析，我发现雇主在数据科学家中寻求的前三种编程语言是 Python(在 90.4%的招聘广告中被提及)、R(在 73.4%的招聘广告中被提及)和 SQL(在 58.5%的招聘广告中被提及)。

![](img/330ebdbba0b2978bbb39f8d2e802c323.png)

这表明，如果您打算为数据科学选择一种编程语言，那么 Python、R 或 SQL 中的一种是最佳选择。

然而，虽然 R 和 Python 都是通用编程语言，具有允许用户执行数据科学的大多数技术要求的附加包，包括统计分析和机器学习，但 SQL 是一种专门为查询和操作关系数据库中的数据而设计的数据库语言。

雇主通常要求 SQL 技能，因为他们将数据保存在关系数据库中，并希望他们的数据科学家能够访问这些数据。他们实际上并不期望他们的数据科学家使用 SQL 执行他们工作的其他方面，比如模型开发。

虽然我之前已经在这里写了关于学习使用数据库的基础知识的重要性，但是作为一名数据科学家，你不需要学习太多的 SQL。只需学习足够的 SQL，以便能够合并和过滤一组表，然后将注意力集中在 Python 或 r 中的一个上。

顺便说一下，有多个为 Python 和 R 编写的包，允许用户从这些语言中运行 SQL 查询(例如，Python 中的 sqlite3 和 R 中的 RSQLite)，因此，为了最大限度地提高效率，您可以在学习 R 和 Python 之一的同时学习 SQL *。*

# #2:其他人都在用什么编程语言？

如果你已经与其他数据科学家或数据专业人员在一个环境中工作，那么最好的学习语言往往是你周围每个人都在使用的语言(即使你已经知道一些不同的东西)。

这样做的原因是因为它将您置于这样一个位置，您可以向您周围更有经验的程序员学习，并得到他们的指导(同时也不会因为您选择的编程语言而受到嘲笑——对一些人来说，整个 R vs Python 的辩论可能变得非常政治化)。

你可以让其他程序员检查你的代码；使用他们的代码作为好的编程技术的模板；从你周围的对话中获取编程的一般技巧。

我的一个朋友曾经告诉我一个她的前同事的故事，他坚持用一种他周围没有人熟悉的语言编程。他在一家跨国保险公司找到了一份工作，在那里他继续保持这种立场，并最终犯下了一个巨大的错误，这让他丢掉了工作，因为没有人能够审查他的工作。

如果你刚刚起步，或者不与任何其他程序员一起工作，那么你可以在更大的层面上应用这种考虑。数据科学社区中的其他数据科学家通常使用什么语言？

在我对 2018 年度 StackOverflow 开发者调查(可在此处找到)进行的分析中，我发现，在自称为数据科学家的受访者中，Python 是最受欢迎的语言，76.8%的人在过去 12 个月中使用过 Python。

相比之下，去年只有 34.0%的人使用过 R，排在 SQL、HTML、JavaScript、CSS、Bash/Shell、Java 和 C++之后。

![](img/f8f288c406f2e9199c4effe70e5e7469.png)

同样，对 [Kaggle 2018 ML & DS 调查](https://www.kaggle.com/kaggle/kaggle-survey-2018)回复的分析显示，在认为“可能”或“肯定”是数据科学家的受访者中，60.5%最常使用 Python(使其成为最受欢迎的语言)，R 以 16.0%的比例位居第二。

# #3:你打算用这种语言做什么？

r 最初是 S/S-Plus 的开源实现，S/S-Plus 是一种专门为统计人员设计的编程语言，通常在大学水平的统计课程中讲授。

尽管 S/S-Plus 的编写使得大部分主要功能都在核心程序中，但 R 被设计成可通过包进行扩展，并且随着时间的推移，已经编写了额外的包来扩展 R 的功能，使之超越统计技术。然而，由于它的起源，R 的优点仍然是它的统计功能。

相比之下，Python 最初是一种通用编程语言，受 C/C++和 Java 的影响，供软件开发人员使用。与 R 一样，Python 也可以通过包进行扩展，但是由于这种语言的通用性质，它的优势在于这些包所提供的功能的广度。

Python 是许多大学计算机科学课程(尤其是与机器学习或人工智能相关的课程)的首选语言，实现非统计功能的包往往首先用 Python 编写，R 包随后创建(要么原生于 R 中，要么作为 Python 包的 R 接口，如谷歌的深度学习包 Tensorflow 的情况)。

一般来说，如果你学习编程语言的目的是专门用于统计分析和建模，那么 R 可能比 Python 更能满足你的需求。

但是，如果您计划扩展到统计之外，特别是数据科学的计算机科学方面(包括机器学习、深度学习、自然语言处理和计算机视觉)，那么请考虑使用 Python。

# #4:未来呢？

引用*搏击俱乐部*的话，“在一个足够长的时间线上，每个人的存活率下降到零”，这也适用于编程语言。不管一种编程语言今天有多流行，最终会有另一种语言取代它。

从积极的一面来看，尽管编程语言时好时坏，但支撑大多数编程语言的原则往往保持不变。

一旦您掌握了函数、for 和 while 循环、if/else 语句和变量类型背后的概念，您就可以相对较快地掌握任何编程语言的基础知识。

尽管如此，如果你打算花时间学习一门编程语言，你希望能够尽可能获得最大的投资回报，这意味着选择一门越来越受欢迎的编程语言，而不是越来越不受欢迎。

数据科学网站 KDnuggets 对其用户的软件选择进行了年度调查(例如，见[这里](https://www.kdnuggets.com/2019/05/poll-top-data-science-machine-learning-platforms.html))。最近三年，Python 在这项民意调查中一直名列前茅，在 2015 年至 2019 年的五年中，其使用量从 30.3%的受访者增长到 65.8%的受访者。

相比之下，在同一时期，R 的使用率从 2015 年的 46.9%增加到 2017 年的 52.1%，然后再次下降，到 2019 年降至 46.6%。

在截至 2019 年 8 月的五年中，谷歌趋势对搜索词“Python”和“R”进行了比较，结果显示，尽管“Python”一直是更受欢迎的搜索词，但“R”的受欢迎程度保持相对平稳，而“Python”的受欢迎程度则大幅上升。

![](img/e5f6037a31f47a2a45980e8e68735a33.png)

因此，如果未来的可用性是你最关心的，那么 Python 就是你要走的路。

# #5:你最喜欢哪种编程语言？

开源语言的美妙之处在于，任何人都可以免费下载它们，并在自己的电脑上使用它们。你不会在没有试驾的情况下购买一辆新车，那么为什么不在选择编程语言时应用同样的原则呢？在接下来的几年里，你可能会花很多时间来使用编程语言。

r、Python 以及其他许多在数据科学家中流行的语言都是开源的。你可以下载你感兴趣的每一种语言，然后，对于每一种语言，花一周左右的时间学习一些你可以在网上找到的入门教程。

一旦你掌握了语法，给自己设定一些基本的任务来进行语言的比较。例如，给定一个你从某个来源下载的数据集，比如 [Kaggle](https://www.kaggle.com/datasets) 或者 [UCI 机器学习库](https://archive.ics.uci.edu/ml/index.php)，你可以尝试下面的方法:

*   加载数据集，计算基本汇总统计数据(如各变量的均值和方差)；
*   单独或成对绘制每个数据变量；
*   进行基本的数据清理，将数据整理成适合模型拟合的形式；和
*   将几种不同的机器学习模型(例如，线性回归模型、决策树、支持向量机和神经网络)与数据进行拟合，并选择最佳模型。

在这个过程的最后，选择最适合你的语言。

# #6:专有语言呢？

到目前为止，本文主要关注的是开源语言，但是它们的专有表亲(即与商业软件相关联的语言)，比如 SAS，情况又如何呢？

虽然曾经有一段时间，甚至就在五年前，雇主倾向于选择商业软件而不是开源软件，但随着开源工具的日益流行，人们的态度已经发生了变化。

据我所知，一些组织(包括跨国咨询公司和企业)正在从商业分析软件转向开源软件，以削减成本。

[的这篇文章](https://thomaswdinsmore.com/2018/03/07/sas-is-on-the-brink-of-something/)反映了这一观察结果，文章讨论了行业从 SAS 到开源工具的转变，并声称“新毕业生进入职场普遍更喜欢 Python 和 R，而不是 SAS。”

如果这还不足以阻止您学习专有编程语言，请记住，专有语言的功能往往比开源语言少，任何超出基本功能的附加功能通常都是以昂贵的附加模块的形式出现的。

此外，如果你学习了一种特定的语言，然后找到了一份工作，而你的新雇主没有你使用这种语言所需的软件，那么说服你的雇主为你提供免费的开源工具要比购买一种商业产品的许可证容易得多，后者每年可能要花费五六位数的费用。

为数据科学选择一种编程语言可能是一个困难的决定。我个人更喜欢 Python，因为它的功能广泛，在数据科学社区很受欢迎，并且有增长的轨迹。然而，至少在中短期内，我预计 Python 和 R 将继续作为两种顶级数据科学语言共存。

所以，只要你学会了其中一个，你就不会错得太多(事实上，如果你对数据科学很认真，那么最终你应该两个都学)。

然而，无论你选择哪种编程语言，一定要学好它。因为，归根结底，重要的不是你用于数据科学的语言，而是你用它做了什么。

*Genevieve Hayes 博士是数据科学家、教育家和人工智能及分析专家，拥有*[*Genevieve Hayes Consulting*](https://www.genevievehayes.com/)*。你可以在*[*LinkedIn*](https://www.linkedin.com/in/gkhayes/)*或者*[*Twitter*](https://twitter.com/genevievekhayes)*上关注她。她还是* [*价值驱动数据科学*](https://www.genevievehayes.com/episodes/) *的主持人，这是一个每月两次的播客，面向希望最大化其数据和数据团队价值的企业。*

*想要发掘企业数据的价值，但不知道从哪里开始？**[***下载免费的数据科学项目发现指南。***](https://www.genevievehayes.com/discovery-guide/)*