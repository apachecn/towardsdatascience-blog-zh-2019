# 相关性并不意味着因果关系。现在怎么办？

> 原文：<https://towardsdatascience.com/the-turf-war-between-causality-and-correlation-in-data-science-which-one-is-more-important-9256f609ab92?source=collection_archive---------26----------------------->

## 实验和因果推理

## 数据科学中因果关系和相关性之间的地盘之争

![](img/8fe951e8a17c4ba6e5993bb540a2355e.png)

Photo by [jean wimmerlin](https://unsplash.com/@jwimmerli?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/fight?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

***2021 年 2 月 20 日更新***

数据科学家知道“相关性并不意味着因果关系”这一警告。仅这个月，Medium 就推荐了 20 多篇包含这句流行语的帖子。在检查了写作语气后，这些帖子暗示或大声说出:

> 相关性不如因果性！

数据世界中“偏向”因果关系的趋势是可以理解的，因为需要多年的专业训练才能掌握因果关系的要点。相比之下，相关研究的门槛较低。

在应用方面，许多业务场景需要因果洞察，包括确定目标受众，迭代未来产品，以及对客户行为产生可操作的洞察。

然而，这些不应该成为我们拒绝相关研究和轻视它的理由。每一种工作都有广泛的应用。

## 第一部分:概念 101

## **1。相关性**

最简单的形式是，事件 A 和 B 一起发生，但没有因果关系。换句话说，我们不知道是 A 导致了 B 还是 B 导致了 A。

例如，一家在线预订机构(如 booking.com)刚刚花了 100 万英镑，在 11 月 10 日推出了一个新的网页设计，一周后网站流量激增。事件 A(新的网页设计)和事件 B(流量激增)是有关联的，但我们不知道是否有因果关系。

UX 的设计师们正不耐烦地等待着，想要获得荣誉。

## **2。因果关系**

除了相互关联，因果关系还增加了两层额外的要求:一个时间顺序和没有选择。在上面的例子中，一个因果断言表明事件 A 由于两个原因导致了事件 B。第一，A 发生在 b 之前，第二，网站流量峰值应该没有替代解释，需要验证。

## **3。替代解释**

数据科学家与产品团队合作，对流量激增提出了另外三种可能的解释:

***假设 1:过去三个季度在数字营销方面增加的支出终于有了回报。***

***假设二:宏观经济状况改善提振客户出游意愿。***

***假设三:又到了一年中旅游的时候了。顾客开始计划圣诞节的家庭旅行。***

这是这两种方法的不同焦点:相关学派只告诉我们这些事件有多紧密的联系，但不能决定是否有因果关系或因果关系的方向；因果学派需要解决这些难题。

为了排除替代方案，数据科学家选择以下三种途径之一:实验、准实验和观察设计。

## 第二部分:三种因果方法

## 解决方案 1:实验设计

对于核心的因果“推理者”，因果推理的黄金标准是**随机控制试验**，随机将研究对象分配到实验条件下，以消除偏差，并将差异归因于治疗。

在上面的 web 流量案例中，我们可以运行一个 A/B 测试，然后**随机**分配来自不同地区的客户接收新设计或旧版本。

然而，细节决定成败。

从技术上讲，随机分配应该消除协变量偏差，并创建平衡的数据分布。然而，考虑到社交媒体对人们生活的渗透，这很容易产生溢出效应。我们都在网上发布我们吃什么，穿什么，做什么的图片，这可能会淡化甚至使因果关系无效。

然而，数据科学家应该适当注意实验的缺点，包括:

1.  **耗时**:运行和收集数据需要很长时间。
2.  **伦理**:我们不能随机分配人吸烟，跟踪得癌症的比率。脸书因网上负面情绪实验而受到抨击。
3.  **对有效性的威胁**。不可能消除****的溢出效应**。**
4.  ****财务成本**。招聘 1000+人，进行现场实验，需要多少钱？对于在线实验，成本也值得注意。设计糟糕的网络实验会让公司损失数百万美元。**
5.  ****工程和数据人力。**您的组织是否有必要的工程人员来实施全面的在线实验？权力分析让你想起什么了吗？如何在治疗效果小的同时减少方差？如何找到在线实验的最佳停止时间？**

## ****解决方案 2:准实验设计****

**由于上面列出的原因，不可能每次都采用 RCT，我们可以满足于准实验设计。对于这种类型的设计，研究人员不能完全控制随机分配，我们可能不得不处理不平衡的协变量分布。**

**在一系列博客文章中，我介绍了多种准实验方法来确定因果关系。**

**[**回归间断设计**](/the-crown-jewel-of-causal-inference-regression-discontinuity-design-rdd-bad37a68e786) **:****

**[](/the-crown-jewel-of-causal-inference-regression-discontinuity-design-rdd-bad37a68e786) [## 回归不连续设计:因果推理皇冠上的宝石

### RDD R 代码完全指南

towardsdatascience.com](/the-crown-jewel-of-causal-inference-regression-discontinuity-design-rdd-bad37a68e786) 

[](/what-is-the-strongest-quasi-experimental-method-interrupted-time-series-period-f59fe5b00b31)****:****

**[](/what-is-the-strongest-quasi-experimental-method-interrupted-time-series-period-f59fe5b00b31) [## 中断时间序列实践指南

### 基础、假设、优点、限制和应用

towardsdatascience.com](/what-is-the-strongest-quasi-experimental-method-interrupted-time-series-period-f59fe5b00b31) 

[](/does-minimum-wage-decrease-employment-a-difference-in-differences-approach-cb208ed07327)****:****

**[](/does-minimum-wage-decrease-employment-a-difference-in-differences-approach-cb208ed07327) [## 差异中的差异方法实践指南:工资上升，就业率下降？

### 大卫·卡德和阿兰·B·克鲁格 1994 年 NBER 工作文件的副本

towardsdatascience.com](/does-minimum-wage-decrease-employment-a-difference-in-differences-approach-cb208ed07327) 

所有的准方法(如 DID、RDD、ITS 等。)分享相同的设计理念:考虑治疗组和对照组之间的任何先前差异，并找到排除它们的方法。我们可以从时间(即今天对比昨天，面板数据)和空间维度(即对比其他类似案例，横截面数据)寻求帮助。

在选择最合适的方法之前，我们必须检查可用的资源和限制。如果应用正确，这些准方法得出的因果推论接近 RCT。** 

## **解决方案 3:观察设计**

**观察方法提供了最后的手段。研究人员不知道数据生成过程，也无法控制干预任务。这就是为什么观察方法经常产生不精确和有偏见的估计。**

**例如，脸书数据科学团队比较了实验方法和非实验方法的性能。他们发现观察法在评估广告测量方面表现不佳。**

## **第三部分:商业伙伴**

**运行实验是昂贵的，并且观察方法是不可靠的。**

**商务人士应该怎么做？**

**一如既往，我推荐以下**迭代**步骤:**

1.  **运行一个小型实验。**
2.  **坚持一段时间，收集一些初步的发现。**
3.  **留意任何更新:新的和不同的东西，还是老样子？**
4.  **如果出现差异，调整工作流程，例如，回到您的业务问题，收集新的变量/数据等。**
5.  **假设时间框架内没有任何变化，那么恭喜你。我们只是测试了我们的假设，而没有对 1000 多万客户进行 A/B 测试。**

> **总是回到我们的业务问题/假设来验证我们的模型。**
> 
> **始终保持迭代工作流。**

**我们可以立即获得有用的发现，以帮助产品团队开始工作，并在需要时进行小的校准。**

**大型科技公司已经将实验性思维融入到他们的商业战略和产品开发管道中(查看这些令人难以置信的工作: [**【脸书】**](https://medium.com/facebook-research/how-quantitative-ux-research-differs-from-data-analytics-1bbf0903768b)**[**网飞**](https://medium.com/netflix-techblog/its-all-a-bout-testing-the-netflix-experimentation-platform-4e1ca458c15)**和**[**Airbnb**](https://medium.com/airbnb-engineering/experiments-at-airbnb-e2db3abf39e7))。********

# ****第四部分:哪个更重要？****

## ******声音 1:为什么是因果关系？******

****因果推理为今天和明天带来好处。****

****因果关系研究显示用户如何参与我们的产品，并量化参与度，**为今天提供可操作的见解。******

****随着时间的推移，人类会改变他们的行为，企业也会随之改变。纵向因果工作帮助我们跟踪这种变化，**预测明天的未来趋势。******

## ******声音 2:为什么要关联？******

****相关研究有更广阔的市场，有更多的商业场景。之所以如此，是因为相关性研究不需要那么“挑剔”的统计假设。****

****比如大零售公司安排店面布局，把相似的产品放在一起。****

****据我所知，**塔吉特、沃尔玛、好市多**都是根据联想分析来重新布置店面的。****

****你可能听说过尿布-啤酒综合症:新爸爸们在从商店出来的路上为他们的新生儿买了尿布后，拿了一杯冰啤酒。于是，商家**在**附近放上帮宝适和百威，捆绑销售。****

> ****老实说，购物对男人来说太沉重了。****

****D-B 综合症是一个商业场景，我们关心的是**什么**产品一起卖，而不是**为什么**。****

****有些项目可能有很好的相关性，但更多的时候是没有原因的。他们就是这样，不知道为什么也没关系。所以，强相关性就足够好了。****

> ****事情是有原因的。****
> 
> ****事情都是无缘无故相关的。****

## ****声音 3:何时以及如何使用？****

******对于因果关系:******

*   ****为什么顾客只浏览商品目录，却从不在沃尔玛完成交易？****
*   ****新的网页设计会如何影响顾客的忠诚度和满意度？****
*   ****为什么用户会脱离产品？****
*   ****为什么新兴市场的顾客只在线下购物，不在网上购物？****
*   ****对于所有其他与为什么和如何相关的问题。****

******进行关联:******

*   ****除了帮宝适和百威淡还有哪些产品一起卖？****
*   ****在好市多商店的什么地方可以设置美食广场？****
*   ****在哪里再开一家星巴克，再开一家亚马逊仓库？****
*   ****生命科学。医生不了解某些疾病是如何发展的，而是依靠相关的体征和症状进行诊断。****
*   ****个性化推荐系统。亚马逊采用的是单品到单品的协同过滤系统。它分析过去的浏览/购买历史，并向顾客推荐相关商品。****
*   ****对于其他数百万不需要知道为什么和如何的问题，相关性设计是首选。****

# ****外卖食品****

****与其问哪个更重要，我们应该问的真正问题是:****

> ****1.各校各有什么利弊？****
> 
> ****2.我们有什么可用的信息？我们面临哪些限制？****
> 
> ****3.如何以及何时采用每一种？****

*****Medium 最近进化出了自己的* [*作家伙伴计划*](https://blog.medium.com/evolving-the-partner-program-2613708f9f3c) *，支持像我这样的普通作家。如果你还不是订户，通过下面的链接注册，我会收到一部分会员费。*****

****[](https://leihua-ye.medium.com/membership) [## 阅读叶雷华博士研究员(以及其他成千上万的媒体作家)的每一个故事

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

leihua-ye.medium.com](https://leihua-ye.medium.com/membership)**** 

## ****实验和因果推理****

****[](/online-controlled-experiment-8-common-pitfalls-and-solutions-ea4488e5a82e) [## 运行 A/B 测试的 8 个常见陷阱

### 如何不让你的在线控制实验失败

towardsdatascience.com](/online-controlled-experiment-8-common-pitfalls-and-solutions-ea4488e5a82e) [](/why-do-we-do-and-how-can-we-benefit-from-experimental-studies-a3bbdab313fe) [## 数据科学家应该有充分的理由进行更多的实验

### 好的，坏的，丑陋的

towardsdatascience.com](/why-do-we-do-and-how-can-we-benefit-from-experimental-studies-a3bbdab313fe) 

# 喜欢读这本书吗？

> 请在 [LinkedIn](https://www.linkedin.com/in/leihuaye/) 和 [Youtube](https://www.youtube.com/channel/UCBBu2nqs6iZPyNSgMjXUGPg) 上找到我。
> 
> 还有，看看我其他关于人工智能和机器学习的帖子。********