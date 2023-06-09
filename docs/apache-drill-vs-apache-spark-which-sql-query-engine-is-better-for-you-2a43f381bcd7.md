# Apache Drill 与 Apache Spark —哪个 SQL 查询引擎更适合您？

> 原文：<https://towardsdatascience.com/apache-drill-vs-apache-spark-which-sql-query-engine-is-better-for-you-2a43f381bcd7?source=collection_archive---------15----------------------->

> 原文发布于此:[https://blog . contact sunny . com/tech/Apache-drill-vs-Apache-spark-which-SQL-query-engine-is-better-for-you](https://blog.contactsunny.com/tech/apache-drill-vs-apache-spark-which-sql-query-engine-is-better-for-you)

![](img/cb3cbefcc4ba137d4d19c6bdcbf9f2c8.png)

如果您在大数据、数据科学或 BI 领域，您可能听说过 Apache Spark。你们中的一些人可能也听说过 Apache Drill，你们中的一小部分人可能实际上使用过它。我最近发现了 Apache Drill。但从那以后，我开始喜欢它所提供的东西。但是当我浏览 Apache Drill 的功能时，我想知道的第一件事是，它与 Apache Spark 有什么不同？我能互换使用这两个吗？我做了一些研究，找到了答案。在这里，我将回答这些问题，为我自己，也许也为你们。

理解这两者之间的根本区别、它们是如何实现的以及它们能够做什么是非常重要的。

使用 Apache Drill，我们编写 SQL 查询来从各种来源获取数据，例如 SQL 数据库、MongoDB、AWS S3、Apache Kafka、JSON 文件等等。但是使用 Apache Spark，我们编写“类似 SQL”的查询来从各种数据源获取数据。这里的区别在于，Drill 是一个 ANSI SQL:2003 查询引擎，具有比传统 SQL 查询引擎更强大的功能。另一方面，Apache Spark 只支持 SQL 查询的一个子集，而且是有限的。Spark 是一个通用的计算引擎，它支持类似 SQL 的查询来获取运行这些计算所需的数据。Spark 还为您希望运行查询的各种存储服务提供了驱动程序。

SparkSQL 支持的数据源列表也相当长，但没有 Drill 那么长。长期使用 BI 工具的人会发现自己对 SQL 查询驾轻就熟。将这些知识带到 Apache Drill 中，将使他们能够从对他们来说可能是新的数据源中查询数据，如 NoSQL 数据库、拼花文件、S3 文件等。这样的人可以使用 Apache Drill 运行复杂的聚合查询；而且大多数时候，他们得到了他们需要的结果。SparkSQL 就不一样了。

SparkSQL 非常适合在 Spark 内部处理数据，并且希望通过一些简单的连接和 *where* 条件从外部数据源获取数据。一旦将数据放入 Spark 数据集，就可以应用转换并执行操作。

这两个工具处理底层数据的方式非常不同。Apache Drill 能够接受在多个数据源上运行的复杂查询，并且能够将这些查询下推到相关数据源的本地驱动程序。它在内部将数据映射为 JSON 格式，并且它使用 JSON 的能力使得 Drill 在某种程度上比 Spark 更加灵活。

Drill 还使用 FLATTEN 和 KVGEN 等命令扩展了 ANSI SQL 查询，这使得处理简单甚至复杂的 JSON 数据变得更加容易。由于 Drill 在内部使用 JSON，它使 Drill 能够动态地发现模式。

总之，如果您想做大量的数学、数据转换和机器学习工作，最好坚持使用 Apache Spark。如果不是这样，而您只想运行一些聚合查询来分析数据，那么您可以使用 Apache Drill。

有意思的是，Drill 支持 JDBC 驱动，Spark 可以在 SparkSQL 内使用 JDBC 驱动来取数据。因此，如果您希望对导入 Spark 的数据进行精细控制，并希望对这些数据进行复杂的转换，您可以使用 Spark 中的 Drill 将数据导入 Spark。这种组合对于大多数应用来说应该足够了。