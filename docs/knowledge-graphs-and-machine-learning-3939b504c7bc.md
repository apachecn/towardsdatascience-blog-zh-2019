# 知识图和机器学习

> 原文：<https://towardsdatascience.com/knowledge-graphs-and-machine-learning-3939b504c7bc?source=collection_archive---------8----------------------->

![](img/cfaa578e46e16629e5aad7356bdbea85.png)

## **半自动洞察生成的强大组合**

知识图是一组由描述一个领域(例如一个企业、一个组织或一个研究领域)的关系所链接的数据点。这是一种强大的数据表示方式，因为知识图可以自动构建，然后可以探索以揭示关于该领域的新见解。

知识图谱是*二级*或*衍生*数据集:通过对原始数据的分析和过滤获得。更具体地说，数据点之间的关系是预先计算的，并成为数据集的重要部分。这意味着不仅每个数据点都可以快速、大规模地分析，而且每个关系都可以分析。

> 选择如何描述这种关系以及快速大规模分析的能力是获得新见解的关键。从数据到信息，从信息到知识，从知识到洞察，从洞察到智慧。

例如，地理地图包含城市的名称和坐标，而简单的知识图也包含城市之间的距离。因此，不用在查询时计算所有的距离，我可以直接问:A 点和 R 点之间的最短路径是什么？预先计算距离是一个简单的步骤，但使地理分析更快，也允许轻松测试不同的场景。例如，知道 B 点突然不可到达，A 和 R 之间的最短路线是什么？

图形作为分析工具已经存在了几个世纪，但是直到最近才出现了“知识图”的概念。它的形式定义由 Paulheim ( [2016](http://www.semantic-web-journal.net/system/files/swj1167.pdf) )给出，其中一个知识图:

*   描述现实世界的实体及其相互关系；
*   定义架构中实体的可能类和关系；
*   允许任意实体之间潜在的相互关系；
*   涵盖各种主题。

除了定义之外，知识图还有巨大的市场吸引力:它意味着一个技术人工制品，它封装了一个公司或另一个领域的所有关系，从而导致更好的理解。这正变得越来越真实，这也要归功于机器学习。

## **使用机器学习描述新关系**

机器学习革命的主力是通过深度学习进行数据分类。通过对数据进行分类，我们可以创建属于同一类的相关数据点子集。这种关系在分类之前并不存在，现在可以用来创建知识图。

深度学习的强大之处在于能够对复杂的数据进行分类，而不需要提供明确的描述，只需要简单的例子。图像、语音、文档、电子表格、演示文稿、视频……深度学习可以对许多不同种类的数据进行分类，这为从多个角度描述一个领域提供了前所未有的机会。手动描述数百万个数据点基本上是不可行的。想象一下，必须阅读和分类数百万份精确但枯燥的法律文件。不是对人类时间的最佳利用。

充分利用一个人的时间也是一个公司的 ML 生成的知识图的简单例子:通过分析文档，有可能知道 *A-team* 和*team∈*分别在同一主题上工作，这提供了改进协作的机会。

图形和 ML 的强大组合有许多可能的用例。开发需要在两个具有挑战性的方面下功夫:访问数据和找到将导致期望结果的类。第一个问题主要是组织、法律和伦理问题，而第二个问题需要领域知识。在 ML 革命之前，这通常只能由主题专家提供，而现在 ML 系统可以支持这项工作，降低了准入门槛。

## **ML 也支持关系类的定义**

机器学习可以支持使用分类以及类的定义来创建关系。例如，文档的自然语言处理可以对主题建模并识别命名实体。有了它们的统计表示，人们就可以根据数据来决定哪些元素应该构成新的关系类型。这些然后成为分类的标签。

![](img/ad7a514494f61bf73542639921fb7206.png)

这意味着，为了创建知识图，任何可能包含相关信息的数据库都会被爬行和扫描。文件、目录、活动日志……任何东西都可以进行统计分析，以创建分类和本体，这些术语用于定义数据点之间的类、属性和关系，以及如何创建新的数据点。它们是对所有考虑的数据点进行分类和描述的蓝图和说明。这就是为什么知识图有时也被称为语义网络的核心。*语义*强调了这样一个事实，即表示的*与相应的数据一起编码。这是通过分类法和本体论完成的(它们的通用术语有一些重叠，部分是由于它们的起源。分类学源于生物学，而本体论源于哲学——源于希腊语 *Ontologia，*“对存在的研究”。存在更正式的定义，如计算机科学中使用的定义，但它们在此上下文中并不完全相关)。*

在定义分类法和本体论时，人的判断是很重要的，因为数据可以用无数种方式来描述。机器仍然无法考虑更广泛的背景来做出适当的决定。分类法和本体论就像是提供了一个观察和操作数据的视角。如果没有考虑感兴趣的元素，那么知识图不会提供任何洞察力。选择正确的视角是创造价值的方式。典型地，这个任务是反复执行的，也从失败中学习。

![](img/33fe62d704a9c47596192c8a5685f626.png)

一旦您定义了规则，您就可以将它们应用到新数据，创建元数据，从而创建知识图。在适当的数据库系统中，可以很容易地查询和分析它。例如，一个特定的实体有多少关系？从 A 到 Z 的最短路线是什么？子图有多相似？

知识图的强大之处之一是能够将不同类型的数据和来源联系起来。这对于通过组合来自不同来源的信息来提取价值非常有用，例如跨公司筒仓。

创建知识图是一项重要的工作，因为它需要访问数据、重要的领域和机器学习专业知识，以及适当的技术基础设施。然而，一旦为一个知识图建立了这些需求，就可以为更多的领域和用例建立更多的需求。鉴于可以发现新的见解，知识图是一种从现有非结构化数据中提取价值的变革性方式。[明智使用](https://medium.com/swlh/building-digital-societies-of-tomorrow-47d5793fabb4)。

![](img/13a417c357e0393e84530a4d3db4bd50.png)

*[All photos and images by author]*

如果你读到这里，你可能会喜欢以光速飞行的[](https://medium.com/@nicolarohrseitz/flying-at-the-speed-of-light-6fdd329345e1)***——元宇宙的苍蝇如何帮助解决了一个长期存在的工程之谜。***