# 开普勒& QGIS:开源地理空间工具浅析

> 原文：<https://towardsdatascience.com/kepler-qgis-a-brief-analysis-of-the-open-source-geospatial-tools-5b6308bb5c95?source=collection_archive---------17----------------------->

## 了解它们是如何工作的，它们的特点是什么，以及我们为什么需要一个新工具

![](img/6a3382da9c358b45058c49260ba9a4a7.png)

Earthquakes in California, 2000 to 2018, [kepler.gl](https://kepler.gl/)

# 先说为什么。

为什么我们需要地理空间分析？为什么现在比以往任何时候都重要？

人类大脑主要基于时间、日期和地点来识别信息。例如，“记得我们昨天在剧院见过吗？”或者“你现在在哪里？”其次是“我在大学”。

借助今天的技术——手机、全球定位系统、社交媒体等等——人们可以收集他们周围甚至全球发生的几乎任何事件的地理参考(时间和地点)数据。

地理空间分析正在利用这些数据构建地图、统计图、统计数据和图表，以显示变化是如何发生的以及具体发生在哪里。大规模呈现数据可以揭示我们周围正在发生的重大转变，例如气候变化。地理空间分析的应用包括但不限于供需匹配、气候变化建模、地理营销、更好的 ETA 估计和人口预测。

如今，公司大多使用像 Kepler.gl 和 QGIS 这样的开源工具。虽然这些工具确实适用于地理空间分析的某些方面，但它们需要在其他方面发挥作用。让我们更详细地探讨一下。

# 开普勒

开普勒是一个基于网络的平台，用于可视化大规模位置数据。它是由优步大学的可视化团队创建的，其使命是创建行业级开源框架来增强大数据。有四种主要套装可供使用——Deck、Luma、React map 和 React vis——来制作漂亮的数据驱动地图。**开普勒**用 [deck.gl](https://deck.gl/#/) 打造，利用 [WebGL](https://www.wikiwand.com/en/WebGL) (一种 JavaScript API)更快更高效地渲染大数据。

开普勒仅仅是一个可视化工具。但就像机器人一样，它非常擅长高效地完成特定的工作。它采用 CSV、JSON 和 geoJSON 文件。开普勒的基本流程是，在本地机器上对数据库执行一些操作，如果不在本地机器上，就下载并在开普勒上绘制。

![](img/0f8a492bcfb7eb6586b3d992754fbf97.png)

New York taxi rides via Kepler.gl

![](img/772dde5e28ef2b2463d3f90b73c9e1ff.png)

Layers available

为了使这些可视化更丰富，它提供了几个层，你可以从中选择，这是非常容易的。例如，要使用点图层，您必须从数据中选择纬度和经度列，瞧！不仅如此，你还可以在一层之上添加多层。是不是很酷？

除此之外，您还可以添加过滤器(时间、日期或大小)、选择颜色、设置不透明度、为地图上的点设置轮廓，以及选择查看内置的地图图层，如土地、道路、水和 3D 建筑物。它也有一个比较视图，您可以启用和可视化两个地图并排。

# 然而…

地理空间分析不仅仅是美丽的可视化。正如我之前所说，开普勒目前只提供可视化。一个完整的地理空间分析工具中应该有的许多重要功能都缺失了。其中一些是:

*   您总是不得不手动添加数据文件(电子表格或 geoJSON ),并且无法做出任何实时决策。
*   空间操作是地理空间分析工具的一个重要方面，如合并、连接和聚类在 Kepler 中不可用。不仅合并和连接，而且更简单的计算都必须在外部完成，然后放入 CS 系统。
*   在开普勒，添加不同种类的地图是不可能得到更多的背景。
*   目前，他们提供了自己的一套颜色供你选择，对我来说，这是一个挫折。不可否认，他们有很多选择，但是我喜欢在我的想象中选择我想要的颜色

# 但是等一下…

2019 年开普勒发展路线图承诺了许多新功能，包括高级图层，空间操作和自定义色标。获取完整列表并在此更新。

# QGIS

QGIS 是一个完全开源的桌面软件，由社区维护。安装和使用 QGIS 的成本为零，但这是一个挑战，除非你以前做过，尤其是如果你有其他软件的冲突包。如果你熟悉编程，你甚至可以自己添加功能。它消耗几乎所有类型的数据(超过 70 种矢量格式)。它是跨平台的，可以在所有三种主要的操作系统 Windows、Mac 和 Linux 上使用。

QGIS 就像地理空间世界的**excel**。从创建地图、执行空间操作到使用 QGIS 数据库，您几乎可以做任何事情。它可以用于非常大的项目，从开始到结束的一切，*如果你有一个 GIS 项目，没有其他类型的数据*。它提供了一些插件，可以为你的项目增加一颗额外的星星，其中一些是，

1.  QuickOSM 允许下载 OpenStreetMap 数据
2.  QuickOSM 查询引擎—帮助您从 QuickOSM 插件下载特定数据
3.  数据绘图—允许创建矢量数据的 [D3 图](https://d3js.org/)

# 然而…

QGIS 是迄今为止最丰富和最有用的地理空间分析工具。然而，就像其他工具一样，它也有自己的局限性。而且[我们在现场相信](https://medium.com/locale-ai/why-its-time-for-a-fresh-new-approach-for-real-time-location-based-decisioning-461b3e678fc6)，不仅仅是工具，地理空间数据本身也充满了挑战。

安装和管理 QGIS 是非常不同的，除非你已经这样做了，特别是如果你从其他软件的冲突包。QGIS 难以处理大数据，并且没有真正提供对流数据的支持。在流数据上执行地理空间查询变得非常计算密集型，而我们没有支持它的工具。虽然有时，开发人员会创建他们自己的内部工具集，但这些工具并不适合全球使用，因为它们专注于他们正在执行的特定任务。

此外，当连接到数据库时，它工作得很好，但它是一个桌面应用程序，而不是在云上。此外，如果一个商业人士想使用 QGIS，它不是很直观，因为它需要空间数据知识。该分析不能与任何人共享，不能使用企业规模和更现代的聚合方法，如地理哈希或六边形网格。要知道这些是什么意思，请[参考](/spatial-modelling-tidbits-honeycomb-or-fishnets-7f0b19273aab)这篇文章。

# Locale.ai

那么什么是 Locale，我们为什么要建立它呢？

一切都始于一个个人问题。作为处理地理空间数据的数据科学家，现有的分析产品在我们的日常工作流程中毫无用处。因此，我们必须为我们的日常工作流程构建自己的工具和库。

在这样做的时候，我们意识到不仅仅是我们。谈到位置数据，全球各地的数据科学家都面临着类似的问题。因此，企业正在努力提高运营效率。在[现场](https://www.locale.ai/)，我们计划一劳永逸地解决这个问题。

![](img/d80b84f273c6a3cc40d5ff729ee1fb7d.png)

我们正在努力使位置分析成为整个分析生态系统的一部分。因为当然，位置智能不仅仅是在地图上跟踪和标绘点。您可以混合搭配空间和非空间数据库，并回答您的所有问题。我们的目标是让商业用户在不依赖开发者的情况下获得空间洞察力。

> *位置情报不仅仅是在地图上追踪和标绘点。*

借助我们的平台，您可以大规模传输空间数据，这意味着所有这些都是在大规模、实时和非常精细的级别上进行的。我们还添加了一个拖放界面，为业务用户(不知道如何编写复杂的空间查询)编写复杂的查询，以获得他们问题的答案。您可以使用 Locale 的平台轻松定制您的空间模型。

Locale 在一个地方提供团队专用的控制台。它有警报和触发器，以防有任何异常值，如果您想将数据导出到您的系统中，它还提供 API。

*如果你对这个问题有共鸣，想投稿，我们* [*招聘*](https://locale.freshteam.com/jobs) *不同角色。如果你想深入研究，请查看我们的* [*网站*](https://www.locale.ai/) *或通过*[*hello @ locale . ai*](mailto:aditi@locale.ai)*联系我们！*

*原载于 2019 年 9 月 18 日* [*现场*](https://medium.com/locale-ai) *。*