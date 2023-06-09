# 控制数据密集型(大数据、快速数据)框架的编程语言

> 原文：<https://towardsdatascience.com/programming-language-that-rules-the-data-intensive-big-data-fast-data-frameworks-6cd7d5f754b0?source=collection_archive---------13----------------------->

![](img/92856223bdd27a6d2c2ea2a3203f1816.png)

回到过去，公司主要使用一种主要的编程语言(如 C、C++、Java、c#…)、一种数据库(SQL)和两种数据交换格式(XML、JSON)。自 21 世纪初以来，随着互联网和移动设备的兴起，情况发生了变化。每年，数据的数量和速度都在成倍增长，并继续呈指数级增长。

像*亚马逊*、*谷歌*这样的大型 IT 公司突然发现，现有的工具和框架不足以处理这些大而快的数据。这些公司开发了封闭的源代码框架来处理“网络规模”的数据，并以论文的形式分享他们的概念/架构。2003 年， *Google* 发表了 [**Google 文件系统**](https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf) 论文接着是 [**地图缩小**](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf) 论文和 [**大表**](https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf) 论文。还有，*亚马逊*在 2007 年发表了 [**迪纳摩**](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf) 的论文。由于整个行业面临着处理“网络规模”数据的相同问题，开发人员社区和行业采用了这些论文的概念，并开发了类似 **Hadoop** 生态系统、 **NoSQL** 数据库和其他框架的系统。随着 GitHub 和开源友好性的普及，在接下来的几年中，业界开发并采用了更多的数据密集型框架。

最近我在读一本很棒的书: [**设计数据密集型应用**](http://dataintensive.net/) ，作者是[**Martin Kleppmann**](https://martin.kleppmann.com/)，该书对各种数据密集型框架进行了全面深入的概述。在读那本书的时候，一个问题突然出现在我的脑海里:数据密集型框架中使用最多的编程语言是什么？

在这里，我将尝试在开源数据密集型框架中找到最常用的编程语言。由于有许多数据密集型框架/库，我将主要关注每个类别中的顶级开源框架。此外，如果一个框架/库是用多种语言编写的，我将只选择主要语言。

# 搜索引擎

1997 年， *Doug Cutting* 试图使用当时“刚刚起步”的编程语言 Java 开发一个全文搜索引擎。他在 3 个月内完成了基本功能的开发，并于 1999 年发布了名为 **Lucene** 的 Java 库，用于信息搜索/检索。Lucene 是一个 **Java** 库，不能与其他编程语言集成。Apache Solr 是一个搜索引擎，它提供了一个围绕 Lucene 的 HTTP 包装器，因此它可以与其他编程语言集成。Solr 还通过 SolrCloud 提供可伸缩的分布式全文搜索。和 Lucene 一样，Solr 也是用 Java 开发的，并于 2006 年首次开源。为了给妻子搜索食谱， *Shay Banon* 开发了分布式搜索引擎 **Elasticsearch** (以前的 **Compass** )。Elasticsearch 提供了一个围绕 Lucene 的 RESTful API 以及一个完整的分布式全文搜索栈(ELK)。它于 2010 年发布，用 **Java** 开发。Sphinx 是这个列表中最后一个分布式搜索引擎。早在 2001 年，安德鲁·阿克肖诺夫就开始开发搜索引擎 Sphinx 来搜索数据库驱动的网站。Sphinx 提供 REST 以及 SQL 类(SphinxQL)搜索客户端，并在 **C++** 中开发。

*   Lucene:Java
*   Solr : Java
*   弹性搜索:Java
*   狮身人面像 : C++

# 文件系统

2002 年，*道格·卡丁*和*迈克·卡法瑞拉*在为**纳特**项目工作，抓取并索引整个互联网。2003 年，他们达到了一台机器的极限，并希望在四台机器上扩展它，但面临着在节点之间移动数据、空间分配的问题([**Hadoop 的历史**](http://www.balasubramanyamlanka.com/history-of-hadoop/) [)。](http://www.balasubramanyamlanka.com/history-of-hadoop/).)2003 年， *Google* 发表了其 [**Google 文件系统**](https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf) 的论文。以谷歌论文的蓝图为基础，*道格·卡丁*和*迈克·卡法雷拉*开发了 **Hadoop 分布式文件系统** **HDFS** (当时命名为 NDFS)，它提供了无模式、持久、容错的分布式存储系统。 **HDFS** 在 **Hadoop** 生态系统和大数据框架的开发中发挥了关键作用。尽管 Hadoop MapReduce 正在失去对新框架(Spark/Flink)的吸引力，但 HDFS 仍然被用作事实上的分布式文件系统。像其他 Hadoop 框架一样，它是用 Java 开发的，并于 2005 年开源。在*格鲁斯特公司*中。，*Anand Babu peri Samy*为超大规模数据开发了软件定义的分布式存储 **GlusterFS** 。GlusterFS 于 2010 年开源，用 **C** 编写。受*脸书*论文[大海捞针:脸书的照片存储](https://www.usenix.org/legacy/event/osdi10/tech/full_papers/Beaver.pdf) ，*卢沛宁*实现了一个简单且高度可扩展的分布式文件系统，名为 **SeaweedFS** ，可以存储数十亿个文件。2011 年开源，用 **Go** 编写。另一个强大的分布式存储平台是 **Ceph** ，它提供对象级、块级和文件级存储。Ceph 最初由 *Inktank* 开发，目前由以*红帽*为首的一批公司开发。尽管 Ceph 是在 2006 年首次发布的，但它的第一个稳定版本是在 2012 年。它的文件系统， **CephFS** 是用 **Rust** 编写的，尽管 Ceph 对象存储是用 **C++** 编写的。*德国 Fraunhofer Institute* 开发了一个并行集群文件系统 **BeeGFS** 针对高性能计算进行了优化，重点关注灵活性、可扩展性和可用性。BeeGFS 的第一个测试版本发布于 2007 年。它是用 **C++** 以非常紧凑的方式(约 40k 行代码)开发的。虽然 BeeGFS 是一个并行文件系统，并广泛用于超级计算机，但它可以作为 HDFS 的一个更快的替代方案。

*   [HDFS](https://hadoop.apache.org) : Java
*   [GlusterFS](https://docs.gluster.org/en/latest/) : C
*   [SeaweedFS](https://github.com/chrislusf/seaweedfs) :去
*   [CephFS](http://docs.ceph.com/docs/mimic/cephfs/) :铁锈
*   [BeeGFS](https://www.beegfs.io/content/) : C++

# 成批处理

在开发完**之后，HDFS** 、*道格·卡丁*和*迈克·卡法雷拉*想要在多台机器上为项目**纳特奇**运行大规模计算。受[**Google Map Reduce**](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf)**论文的启发， *Doug Cutting* 和 *Yahoo* 的一个团队开始开发大规模、使用商用硬件的分布式计算， **Hadoop MapReduce** 诞生了。Hadoop MapReduce 和 HDFS 于 2005 年首次开源，取得了巨大的成功，为包括 Yarn、HBase、Zookeeper 等数据密集型框架的整个生态系统铺平了道路。像 Lucene 和 Nutch 一样，Hadoop MapReduce 和几乎整个 Hadoop 生态系统都是用 **Java** 开发的，可以说是将 Java 设定为数据密集型领域事实上的编程语言。如果说 Hadoop MapReduce 开创了大规模分布式计算，那么 **Apache Spark** 是目前最具优势的批处理框架。由著名的 *Berkley AMPLab* 开发，由 *Matei Zaharia* 领导，它解决了 Hadoop MapReduce 框架的局限性(例如，在每次地图作业后存储数据)。Spark 还提供了一种类似于 Unix 的方式，将多个作业组成一个数据处理管道，并为开发人员提供友好的 API，使用 *RDD、数据集、数据帧*对分布式任务进行编程。Spark 主要在 **Scala** 中开发，2014 年发布。Apache Flink 是另一个非常流行和有前途的集群计算框架。和 Spark 一样，也来自学术界，起源于*图柏林*大数据项目**同温层**。与批处理优先框架 Spark 不同，Flink 是流优先框架，将批处理作业作为流的特例来处理。像 Spark 一样，Flink 也提供开发人员友好的 API，使用*数据集、数据流*对分布式计算进行编程。Flink 主要用 **Java** 编写，2015 年发布。**

*   **[Hadoop MapReduce](https://hadoop.apache.org) : Java**
*   **[火花](https://spark.apache.org/) : Scala**
*   **Flink : Java**

# **流处理**

**Hadoop MapReduce 发布后，被社区广泛接受，公司开始使用 Hadoop MapReduce 处理大规模数据。不久之后，公司需要实时分布式流处理框架，因为在现实中，数据主要以流的形式产生。由于许多因素(例如容错、状态管理、定时问题、窗口等)，实时处理大规模数据流比处理批处理作业更困难。第一个开源实时分布式流处理框架是由 *Nathan Marz* 开发的 **Apache Storm** ，并在 2011 年发布，口号是“实时的 Hadoop”。它是用 **Java** 开发的。此外，Apache Spark 还提供了一个流处理框架“ **Spark Streaming** ”,它使用微批处理方法进行流处理，具有接近实时的处理能力。如果 Apache Storm 是普及分布式流处理的框架，那么 **Apache Flink** 将分布式流处理向前推进了一步，可以说是当前分布式实时流处理的领导者。除了低延迟流处理，它还提供了一些创新和高级功能，如状态管理、一次处理、迭代处理和窗口。另一个有趣的分布式流处理框架是由 NSA 于 2006 年开发的 Apache NiFi。虽然它不提供像 Flink 那样的高级流处理特性，但对于大规模数据的简单用例来说，它是一个非常有用的框架。Apache NiFi 也是用 **Java** 开发的，2014 年开源。 **Apache Samza** 是在 *Linkedin* 中开发的这个列表中的最终流处理框架。Samza 提供了一些高级的流处理特性，但是与 Apache Kafka 和 Yarn 紧密结合。它也是用 Java 开发的，并于 2005 年发布。**

*   **[风暴](http://Stream Processing: After the release of Hadoop MapReduce, it was widely accepted by the community and companies started to process their large-scale data with Hadoop MapReduce. Soon after, companies needed Real Time distributed Stream processing frameworks because in reality, data is produced mainly as Stream. Processing Stream in Real Time for large scale data is more difficult than processing Batch job due to many factors (e.g. Fault Tolerance, State Management, Timing issues, Windowing ...). The first open source Real Time distributed Stream processing framework was Apache Storm released in 2011 with the slogan "The Hadoop of Real-Time". It was developed in Java. Also Spark offers a Stream processing framework „Spark Streaming“ which uses Micro-Batch approach for Stream processing with near Real Time processing. If Apache Storm was the framework that popularized the distributed Stream processing, then Apache Flink has taken distributed Stream processing one step further and is arguably the current leader in distributed Real Time Stream processing. Along with low latency Stream processing, it additionally offers some innovative and advanced features like State Management, exactly once handling, Iterative processing, Windowing. Another interesting distributed Stream processing framework is Apache NiFi developed by NSA in 2006\. Although it does not offer advanced Stream processing features like Flink, it is a very useful framework for simple use cases with large scale data. Apache NiFi also developed in Java and open sourced in 2014\. Apache Samza is the final Stream processing framework in this list which offers some advanced features but tightly coupled with Apache Kafka and Yarn. It is also developed in Java and released in 2005\. •	Storm (http://storm.apache.org/): Java •	Spark (https://spark.apache.org/): Scala •	Flink (https://flink.apache.org/): Java •	NiFi (https://nifi.apache.org/): Java •	Samza (http://samza.apache.org/): Java  Messaging:  Messaging is one of the preferred ways to communicate between processes/Micro Services/systems because of its asynchronous nature. Predominantly, messaging is implemented via a Queue where producers write messages in Queue, consumers read messages from Queue and once all consumers read the message, it is deleted from the Queue (fire and forget style). When Linkedin had broken their very large Monolith application to many Micro Services, they had the issue of handling data flow between the Micro Services in a scalable way without any single point of failure. A group of Linkedin Engineers (Jey Kreps, Neha Narkhede, Jun Rao) have used distributed Log (like write ahead log in Databases) instead of Pub/Sub Queue for messaging and developed Apache Kafka. Like File systems or databases in Batch processing, Kafka works as a “single source of truth” in the Stream processing world and used heavily for data flow between Microservices. Kafka is developed mainly in Java and first open sourced in 2011\. Yahoo has developed Apache Pulsar as a distributed Messaging framework which offers both Log based messaging (like Kafka) and Queue based messaging. Apache Pulsar was open sourced in 2016 and mainly developed in Java. Rabbit Technologies Inc. has developed the traditional Queue based Pub-Sub system RabbitMQ. It was first released in 2007 and developed using Erlang. ActiveMQ is another Queue based Pub-Sub system which implements the Java Message Service (JMS). It was initially developed by the company LogicBlaze and open sourced in 2004\. ActiveMQ is developed in Java. A relatively new but very promising Queue based distributed pub-sub system is NATS. It is developed by Derek Collison in CloudFoundry on a weekend using Ruby. NATS was released in 2016 and later reimplemented in Go.  •	Kafka (https://kafka.apache.org/): Java •	Pulsar (https://pulsar.apache.org/): Java •	RabbitMQ (https://www.rabbitmq.com/): Erlang •	ActiveMQ (http://activemq.apache.org/): Java •	NATS (https://nats.io/): Go  Databases:  I have used the DB-Engines ranking (https://db-engines.com/en/ranking) to get the top 5 distributed databases of 21st century. According to this ranking, MongoDB is ranked 5th and only superseded by the Big Four SQL databases. MongoDB is a distributed document-oriented database developed by 10gen (currently MongoDB Inc.) and released in 2009\. It is one of the most popular and mostly used NoSQL databases written mainly in C/C++. Another hugely popular NoSQL database is Redis which is a distributed key-value store database. Back in 2001, an Italian developer Salvatore Sanfilippo started developing Redis to solve the scalability problem of his startup. Released in 2009, Redis is written in C. Avinash Laskshman (co-author of Amazon Dynamo paper) and Prashant Malik has developed Cassandra in Facebook to improve Facebook’s inbox search. Heavily influenced by the Google's BigTable and Amazon's Dynamo paper, Cassandra was open sourced by Facebook in 2008\. Cassandra is both a distributed key-value store and wide column store which is predominantly used for time series or OLAP data and written in Java. Part of the Apache Hadoop project, HBase is developed as a distributed wide column database and released in 2008\. Like almost the whole Hadoop ecosystem, HBase is developed in Java. Neo4j is the final NoSQL database in this list and de-facto standard as Graph Database. Developed by Neo4j, Inc, it was released in 2007 and written in Java. •	MongoDB (https://www.mongodb.com/): C/C++ •	Redis (https://redis.io/): C •	Cassandra (http://cassandra.apache.org/): Java •	HBase (https://hbase.apache.org/): Java •	Neo4j (https://neo4j.com/): Java) : Java**
*   **[火花](https://spark.apache.org/) : Scala**
*   **[弗林克](https://flink.apache.org/) : Java**
*   **[NiFi](https://nifi.apache.org/) : Java**
*   **Samza : Java**

# **信息发送**

**消息传递是进程/微服务/系统之间通信的首选方式之一，因为它具有异步的特性。消息传递主要是通过队列实现的，在队列中，生产者将消息写入队列，消费者从队列中读取消息，一旦所有消费者都读取了消息，就从队列中删除该消息(触发并忘记风格)。当 Linkedin 将他们非常庞大的应用程序分解成许多微服务时，他们面临的问题是如何以可扩展的方式处理微服务之间的数据流，而不会出现任何单点故障。一群 *Linkedin* 工程师( *Jey Kreps，Neha Narkhede，饶俊*)已经使用分布式日志(就像数据库中的预写日志)代替发布/订阅队列进行消息传递，并开发了 **Apache Kafka** 。像批处理中的文件系统或数据库一样，Kafka 在流处理世界中作为一个“**真实的单一来源**”，大量用于微服务之间的数据流。Kafka 主要用 Java 开发，并于 2011 年首次开源。雅虎已经开发了 **Apache Pulsar** 作为分布式消息传递框架，提供基于日志的消息传递(像 Kafka)和基于队列的消息传递。Apache Pulsar 于 2016 年开源，主要用 **Java** 开发。 *Rabbit Technologies Inc.* 开发了传统的基于队列的发布-订阅系统 **RabbitMQ** 。它于 2007 年首次发布，使用 **Erlang** 开发。ActiveMQ 是另一个基于队列的发布-订阅系统，它实现了 Java 消息服务(JMS)。它最初由 LogicBlaze 公司开发，并于 2004 年开源。ActiveMQ 是用 **Java** 开发的。一个相对较新但非常有前途的基于队列的分布式发布-订阅系统是 NATS。它是由德里克·科利森在一个周末使用 Ruby 在 T42 的 CloudFoundry 开发的。NATS 于 2016 年发布，后来在 **Go** 中重新实现。**

*   **卡夫卡 Java**
*   **[脉冲星](https://pulsar.apache.org/) : Java**
*   **[RabbitMQ](https://www.rabbitmq.com/) : Erlang**
*   **[ActiveMQ](http://activemq.apache.org/) : Java**
*   **[NATS](https://nats.io/) :走**

# **数据库**

**我使用了 [DB-Engines 排名](https://db-engines.com/en/ranking)来获得**21 世纪**的前 5 名分布式数据库。根据这个排名， **MongoDB** 排名第五，仅次于四大 SQL 数据库。MongoDB 是由 *10gen* (目前为 *MongoDB Inc.* )开发的分布式面向文档的数据库，于 2009 年发布。它是最流行和最常用的 NoSQL 数据库之一，主要用 c++(T17)编写。另一个非常流行的 NoSQL 数据库是 Redis，它是一个分布式键值存储数据库。早在 2009 年，意大利开发人员萨尔瓦托勒·桑菲利波开始开发 Redis 来解决他的初创公司的可扩展性问题。Redis 发布于 2009 年，用 **C** 编写。Avinash lask shman(Amazon Dynamo paper 的合著者)和 Prashant Malik 在脸书开发了 Cassandra 来改进脸书的收件箱搜索。深受谷歌 BigTable 和亚马逊 Dynamo 论文的影响，脸书在 2008 年对 Cassandra 进行了开源。Cassandra 既是分布式键值存储，也是宽列存储，主要用于时间序列或 OLAP 数据，用 **Java** 编写。作为 Apache Hadoop 项目的一部分， **HBase** 是作为分布式宽列数据库开发的，并于 2008 年发布。和几乎整个 Hadoop 生态系统一样，HBase 是用 **Java** 开发的。 **Neo4j** 是此列表中的最终 NoSQL 数据库，也是图形数据库的事实标准。由 *Neo4j 公司*开发，2007 年发布，用 **Java** 编写。**

*   **MongoDB : C++**
*   **[Redis](https://redis.io/) : C**
*   **卡珊德拉 : Java**
*   **HBase : Java**
*   **[Neo4j](https://neo4j.com/) : Java**

# **裁决**

**如果我们考虑大多数主流数据密集型框架中使用的编程语言，那么有一个明显的赢家: **Java** 。虽然在早期被批评为缓慢的语言，但 Java 在该领域显然已经超过了 C、C++等近金属语言或 Erlang、Scala 等一些并发友好的语言。这里我列出了 Java 在数据密集型框架中成功的五个主要原因:**

*   ****JVM** :虽然进程虚拟机自 1966 年就存在了，但是 JVM 可以说已经将虚拟机的概念带到了另一个层次，并且在 Java 的流行和 Java 在数据密集型框架中的使用中发挥了巨大的作用。通过 JVM，Java 从开发者那里抽象出底层机器，并给出了第一种流行的“编写一次，在任何地方运行”的编程语言。此外，在代垃圾收集的支持下，开发人员不需要担心对象生命周期管理(尽管它有自己的问题),可以完全专注于领域问题。首先是 Sun，然后是 Oracle，这些年来改进了 JVM，目前 JVM 是久经沙场的庞然大物，通过了时间的考验。这么多语言(例如 Kotlin、Scala、Clojure)也使用 JVM 而不是开发自己的虚拟机是有原因的。**
*   ****语言支持和框架:**Java 是在 C 之后 23 年、C++之后 10 年才开发出来的，*詹姆斯·高斯林*和 Sun 公司显然已经看到了 C/C++的痛点，并试图用 Java 来解决这些问题。Java 从一开始就引入了对多线程、异常/错误处理、序列化、RTTI、反射的语言支持。此外，Java 提供了一个庞大的库生态系统，这使得用 Java 进行软件开发变得更加容易。诚然，在软件架构和算法相似的情况下，C/C++在大多数时候可以远远胜过 Java。但是在很多时候，软件架构和编程范式对应用程序的性能起着更大的作用，而不是编程语言。这就是为什么用 Java 开发的 Hadoop MapReduce 框架比用 C++开发的类似框架要好。**
*   ****开发人员的工作效率:**开发人员的工作效率是业内的圣杯，因为大多数时候，开发人员的时间是比 CPU/内存更昂贵的资源。当 Java 在 1995 年第一次出现时，它比 C/C++更简单、更精简，这导致了更快的开发时间。正如*比雅尼·斯特劳斯特鲁普(C++的创造者)*和[指出的](http://www.stroustrup.com/bs_faq.html#Java)，Java 后来发展成了一种更重、更复杂的语言，但是在 **2000 年到 2010 年**期间，当大多数主流的数据密集型框架被开发出来时，Java 可能是在开发人员的生产力和性能之间取得平衡的最好的语言。此外，开发人员的生产力导致了更短的开发周期，这对于早期的数据密集型框架非常重要。**
*   ****容错:**数据密集型框架的主要目标之一是使用廉价的商品硬件，而不是昂贵的专用硬件。这种方法的缺点是商用硬件可能会出现故障，而容错是数据密集型应用程序的基石。凭借其对错误处理、分代垃圾收集、边界检查和硬件无关编程的内置语言支持，Java 提供了比 C/C++更好的容错能力。**
*   ****Hadoop 因素:**Java 在 Hadoop 生态系统中的使用对 Java 在数据密集型领域的普遍适应起到了很大的作用，并充当了 Java 的广告。由于 HDFS 和 Hadoop MapReduce 可以说是第一个颠覆性的数据密集型框架，后来的框架总是关注它们，并使用 Hadoop proven Java 开发自己的数据密集型框架。**

# **将来的**

**每年，数据的数量和速度都呈指数级增长，带来了新的挑战。此外，数据密集型环境如此多样化，以至于“一个解决方案解决所有问题”的时代已经结束。虽然随着 [**GraalVM**](https://www.graalvm.org/) 和更新的垃圾收集( [**ZGC**](https://wiki.openjdk.java.net/display/zgc/Main) )的出现，Java 将在大数据领域占据主导地位，但是我相信 Java 将会让位于其他一些语言。在未来几年，哪些编程语言可以取代数据密集型框架中的 Java？这里我已经在后续帖子里详细讨论过: [***回归金属:2019 年开发大数据框架 Top 3 编程语言***](https://medium.com/@md.kamaruzzaman/back-to-the-metal-top-3-programming-language-to-develop-big-data-frameworks-in-2019-69a44a36a842) 。**

**如果你觉得这很有帮助，请分享到你最喜欢的论坛( **Twitter，脸书，LinkedIn** )。高度赞赏评论和建设性的批评。感谢阅读！**

**如果你对编程语言感兴趣，也可以看看我下面的文章:**

**[](/top-10-in-demand-programming-languages-to-learn-in-2020-4462eb7d8d3e) [## 2020 年最受欢迎的 10 种编程语言

### 针对求职者和新开发人员的顶级编程语言的深入分析和排名

towardsdatascience.com](/top-10-in-demand-programming-languages-to-learn-in-2020-4462eb7d8d3e) [](https://md-kamaruzzaman.medium.com/top-10-databases-to-use-in-2021-d7e6a85402ba) [## 2021 年将使用的 10 大数据库

### MySQL，Oracle，PostgreSQL，微软 SQL Server，MongoDB，Redis，Elasticsearch，Cassandra，MariaDB，IBM Db2

md-kamaruzzaman.medium.com](https://md-kamaruzzaman.medium.com/top-10-databases-to-use-in-2021-d7e6a85402ba) [](/back-to-the-metal-top-3-programming-language-to-develop-big-data-frameworks-in-2019-69a44a36a842) [## 回归金属:2019 年开发大数据框架的 3 大编程语言

### C++，Rust，用 Java 做数据密集型框架

towardsdatascience.com](/back-to-the-metal-top-3-programming-language-to-develop-big-data-frameworks-in-2019-69a44a36a842)**