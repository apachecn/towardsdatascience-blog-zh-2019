# 解开行为秘密，克服客户流失的极端情况

> 原文：<https://towardsdatascience.com/unlocking-behavioural-secrets-to-overcome-churn-extremes-9c12a7ccc875?source=collection_archive---------19----------------------->

## 了解、预测并最大限度减少客户流失

# 介绍

在新的全球经济中，客户保留已成为当今动荡的商业环境中的一个核心问题，并对许多服务公司提出了重大挑战。尤其令人担忧的是削减成本和激烈的竞争压力。人们越来越担心，没有充分利用现有客户群的公司正处于不利地位。

学术界已经产生了大量的研究来解决这一挑战的一部分——特别侧重于预测客户流失。然而，仍然需要理解企业中存在的对客户流失的各种看法。管理客户关系的核心目的是让企业专注于增加客户群的整体价值，而客户维系是企业成功的关键。

![](img/02ca18e1cef1a7739a5c6f94fcb102d9.png)

(source: [https://www.istockphoto.com](https://www.istockphoto.com/nl))

本博客系列描述了可用于控制客户流失的方法的设计和实现，重点关注主动流失管理，即在预测客户会流失时提前联系客户，并提供旨在防止客户流失的服务或激励。通过采用定性和定量的调查模式，我试图阐明客户流失的预测模型，并提出一个开发主动流失管理计划的框架。

# **问题**

使用简单的保留模型，客户的终身价值是:

![](img/b281c9dba11d64f788aa2b44d8a90ed6.png)

客户流失管理的整个原则的核心是保留的概念，*。在客户层面，流失率指的是客户在给定时间内离开公司的概率。在公司层面，客户流失是指在给定的时间段内，公司客户群中离开的客户所占的百分比。因此，流失率等于 1 减去留存率:*

*![](img/cf465dddedd4ae95fa28df09c8d28f5e.png)*

*然而，对于任何一个简单的保持生命周期价值模型适用的行业，都存在与客户流失相关的某些缺点，即，客户可能会离开，并且如果没有重大的重新获得努力，不会自然返回。这体现在许多服务中，如杂志和时事通讯出版、投资服务、保险、电力设施、医疗保健提供商、信用卡提供商。*

*有两种基本类型的流失:订阅流失和非订阅流失*

***订阅流失**发生在用户或客户签订了一段时间(每月、每年等)合同的企业中。—想想有线电视、网络或电话提供商)，客户选择在合同到期后不再回来。正如定义中所指出的，这很容易定义、预测和预防，因为有一个清晰、明确的客户流失风险窗口，可以集中开展营销活动。*

*![](img/e7d77de564cff5d49340b792a97c54d3.png)*

***非订阅流失**指的是用户或客户可以随时终止与业务关系的事件，他们可以随意来来去去。随着时间的推移，客户可能会逐渐减少购买频率，也可能会突然不再购买。这篇博客将关注防止订阅流失的过程。*

# ***数据采集***

*传统上，客户流失预测是通过简单地测量某种形式的客户身份和客户最后一次互动的日期/时间来评估的。这些数据虽然不太详细，但可以让你建立模型，在基本层面上预测客户流失。然而，现实情况是，在这个最小数据集的基础上添加额外的数据是推荐的，也是非常鼓励的。包含的数据越多，对客户流失的预测就越准确，因此，如果可以的话，也要在数据集中包含一些东西，如用户的静态人口统计信息、特定类型用户行为的细节等。来源越多越好。*

# ***选定数据***

*我将使用“电信客户流失”数据(IBM 样本数据集)来预测留住客户的行为。在这个数据集中，每一行代表一个客户，每一列包含列元数据中描述的客户属性。*

*数据集包括以下信息:*

*   *上个月内离开的客户—这一列称为流失*
*   *每位客户已注册的服务—电话、多条线路、互联网、在线安全、在线备份、设备保护、技术支持以及流媒体电视和电影*
*   *客户账户信息——他们成为客户的时间、合同、支付方式、无纸化账单、每月费用和总费用*
*   *客户的人口统计信息—性别、年龄范围，以及他们是否有伴侣和家属*

# *数据预处理*

*数据预处理是一种数据挖掘技术，用于将原始数据转换成有用和有效的格式。这通常会占到项目总时间的 80%,因为数据是在不同的时间点从多个来源收集的。理解数据中的不同变量是建立直觉的基础。因此，在继续清理不同的拼写或可能丢失的数据之前，建议为这一部分分配足够的时间，以确保一切都是同质的。彻底的探索和清理将在后续步骤中节省时间，尤其是在进行预测的时候。*

*流失分布表明，我们正在处理一个不平衡的问题，因为有更多的非流失用户。大约四分之一的样本不再是客户(图 1)。当我们构建分类模型时，这将会有所暗示。我将在客户流失建模过程中详细介绍。*

*![](img/dc2e22ad20d1a82f3ae8813134ce6807.png)*

# ***数据可视化和特征选择***

*特征提取旨在通过留下代表最具辨别性信息的变量(属性)来减少变量(属性)的数量。特征提取有助于降低数据维度(维度是数据集中具有属性的列)并排除不相关的信息。*

*在特征选择过程中，人们可以修改先前提取的特征，并定义其中与客户流失最相关的子组。作为特征选择的结果，我们可以得到只包含相关特征的数据集。*

*如下图所示，大部分客户流式传输电影和电视流(图 2)。同样，大多数客户使用无纸化账单，没有在线安全保障。*

*![](img/69e7e71cbbe96810b1a38caaa98da6f4.png)*

*下图显示了大多数客户使用单条电话线提供电话服务。光纤互联网连接比 DSL 互联网服务更受欢迎，每种在线服务都有少数用户。样本中约有一半是按月合同，其余一半是一年期和两年期合同(图 3)。*

*![](img/92742a4a7662717cc054a7413da72cda.png)*

*该图的下半部分显示了付款方式和*任期*变量的细分，因为大部分客户的任期最短(0-12 个月)。*

*图 4 总结了相关性分析的结果。一眼就能看出，流失和变量个数是有关系的；具有不同的强度，例如合同类型、总费用、互联网服务等。有时候很明显有因果关系。然而，相关性并不意味着一个变量的变化实际上*导致*另一个变量的变化。在统计学中，你通常需要进行随机的、受控的实验来确定一种关系是因果的，而不仅仅是相关的。*

*![](img/c9e340f1e8068149d0e3f3bb0531be8b.png)*

# ***结论***

*我们已经讨论了流失问题、其原因，以及从探索性数据分析中发现模式和建立直觉的一些方法。下一次，我们将看看预测模型如何识别流失者并揭示他们流失的原因，以及公司如何管理流失。*

*👋感谢阅读。如果你喜欢我的作品，别忘了喜欢，在[中](https://medium.com/@rashidkazmi)关注我。这将激励我为媒体社区提供更多的内容！😊*

# *参考资料:*

*Ascarza 等人(2018):追求增强的客户保持管理:回顾、关键问题和未来方向。斯普林格科学+商业媒体有限责任公司 2017*

*布拉特伯格等人(2008):《数据库营销:分析和管理客户》。起拱石*

*Ghorbani 和 Taghiyareh (2009): CMF:改善客户流失管理的框架。 *IEEE 亚太服务计算大会(IEEE APSCC)**

*韩等人(2011 年):陈，j .，裴，j .，和 Kamber，M. (2011 年)。数据挖掘:概念和技术。数据管理系统中的摩根考夫曼系列。爱思唯尔科学*

*[“主旨-句法-主题”:https://github.com/lonekorean/gist-syntax-](https://business-science.github.io/correlationfunnel/articles/introducing_correlation_funnel.html)[https://business science . github . io/correlation funnel/articles/introducing _ correlation _ funnel . html](https://business-science.github.io/correlationfunnel/articles/introducing_correlation_funnel.html)*

*[https://blogs . r studio . com/tensor flow/posts/2018-01-11-keras-customer-churn/](https://blogs.rstudio.com/tensorflow/posts/2018-01-11-keras-customer-churn/)*