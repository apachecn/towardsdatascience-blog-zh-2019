# 医疗保健中的人工智能不仅改变了医生的诊断工作流程

> 原文：<https://towardsdatascience.com/ai-in-healthcare-not-only-changing-doctors-diagnostic-workflow-fd36778130e5?source=collection_archive---------22----------------------->

## 创造医疗人工智能产品的思维模式正在发生变化

![](img/41e33418039ff712cacca36e740cd11d.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# **简介**

肺炎是一种主要由微生物引起的肺部感染。如世界卫生组织([世卫组织](https://www.who.int/news-room/fact-sheets/detail/pneumonia))所述，“肺炎是全球儿童死亡的单一最大传染性原因，占所有五岁以下儿童死亡的 15%。[……]由细菌引起的肺炎可以用抗生素治疗，但只有三分之一的肺炎儿童获得了所需的抗生素。"

此外，今天已经缺乏所需的放射科医生。每一个现存的都比以前有更多的工作要做。在综合医院，放射科医生正在他们的观察台上每小时手动进行这种肺炎分类。正如《AI in health care》[杂志](https://trimed-cdn.s3.amazonaws.com/digitalissues/aih/2019/2019_02/index.html)中提到的，对于放射科医生来说，像深度学习这样的人工智能方法将“加快和提高他们解读图像的能力”。

关于肺炎 X 射线图像，人工智能(AI)学习方法可以简化医疗工作流程并提高诊断正确率，因为可以在短时间内对数千张图像自动且有效地给出估计，即使是难以人工诊断的图像。有了这样的帮助工具，放射科医生可以专注于其他重要的任务。

此外，根据提到的世卫组织概况介绍，“肺炎影响各地的儿童和家庭，但在南亚和撒哈拉以南非洲最为普遍。”与欧洲或北美等西方国家相比，整个地区的医疗保健覆盖范围并不相同。拥有自动工具将有助于触发必要的医疗或其他干预，即使没有足够的合格医务人员。

那么，创造和交付这种医疗人工智能软件来改善患有肺炎的儿童的状况，以减少五岁以下儿童死亡总数的 15%是必要的吗？

借助一个示例—关于胸部 x 光图像是否显示肺炎的医疗诊断问题(在我的 [GitHub](https://github.com/IloBe/CNN_Thorax-Pneumonia_Classifier) 个人资料中)—我们考虑以下问题:

1.  AI 软件的发展对医疗保健公司意味着什么？
2.  医疗 AI 软件工具需要什么样的工程？
3.  医疗设备制造商在监管环境中工作:人工智能软件需要满足什么样的质量期望？

# **问题 1:**AI 软件的发展对医疗保健公司意味着什么？

由于历史原因，医疗市场在制造和人事政策方面的“大玩家”一直以**硬件为导向**，创造高质量的医疗设备，因为这是必要的。但是今天，这种情况已经改变了，对于公司来说，区别在于软件部分。因此对于制造过程，软件工程应该有更高的优先权，特别是对于人工智能软件工具的创造。为了实现这一点，你需要专门从事这种软件开发和人工智能研究的专家，医疗保健与专业大学和医院合作。

对于软件开发来说，编程概念的方式发生了变化:

*   在**旧世界**中，为了达到期望的结果，需求和决策标准必须被明确地知晓和实现。
*   在使用人工智能的**新世界**中，胸部肺炎的例子使用深度学习神经网络(CNN——卷积神经网络——分类器)来解决所关注的商业问题，而不需要知道和实施任何详细的决策。

![](img/ba50b061ef10858e2535e462380e3851.png)

source¹

该算法用来作出决定的标准不是立即显而易见的，它来自图像数据集。目标是最终算法应该能够为新的、未知的胸部 X 射线图像预测正确的分类。也就是说，用于软件模型训练、验证和测试的数据集本身是最重要的标准之一。

因此，为了保证统一的工作方法和风险最小化，遵守 **CRISP** (跨行业标准流程(数据挖掘))等工程流程就显得尤为重要。这就引出了第二个问题。

# **问题二:**医疗 AI 软件工具需要什么样的工程？

**CRISP** 流程是数据科学领域国际公认的流程。因此，它的应用有助于与监管机构的沟通以及产品的开发。一般来说，解决业务问题的过程分为不同的阶段。

![](img/974e3d5ac64ab978b22392ab2127db2e.png)

CRISP process diagram by SAP²

关于这个周期，整个解决方案流程从业务理解开始，然后是理解和修改现有数据。根据业务需求，这是成功、正确的产品结果的关键部分，这就是团队合作。

关于**肺炎业务问题**，第一发现是影响医疗诊断的**二值图像分类**问题。

*   *存在哪些数据，我们需要获取哪些数据，需要修改到什么程度？*所使用的 [**Kaggle 数据集**](https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia/version/2) 传送已经标记的图像作为训练、验证和测试样本，每个样本包括两个子目录(肺炎、正常)。但是这种分布不符合数据科学的经验法则(70/30 或 80/20)，因此，这种情况已经改变。使用原始数据集会导致关于所选指标的不切实际、不可靠的性能值。因此，新的分布 V2 和 V3 是从原始数据集创建的，V2 数据分别具有 70%的训练样本、10%的验证样本和 20%的测试样本，V3 数据具有 60%的训练样本、20%的验证样本和 20%的测试样本。

![](img/fda325762d5f30e2d0cecc6bf6c2288e.png)

*   哪些程序适合澄清业务问题？此类图像分类问题的最新概念是**深度学习 CNN** 模型架构。他们的算法识别显示肺炎的图像状态的估计，或者不用于未来图像的预测。图像像素及其信息输入(如彩色区域、边缘、对象结构等)被表示为从更一般到更详细的特定特征的隐藏层特征，这些特征被网络“学习”以能够提供这种输出分类估计。这个概念是模仿人类大脑学习和创造信息的方式。
*   *最初使用哪个 CNN 架构模型，要考虑哪些变体，最终选择哪个，为什么？*为特定任务构建和寻找神经网络并非易事。不同的模型通过一些度量标准相互比较和评估。选择对分类问题和数据集公平的评估度量。最终，使用**瓶颈功能**的最佳模型 **RestNet50** 转移模型已经确定。

![](img/571725a9527ffa183651ffaa6be7c7cd.png)

# **问题 3:** 医疗设备制造商在监管环境中工作:人工智能软件需要满足什么样的质量期望**？**

为了引进一种新的医疗产品，必须考虑法律方面的问题。一般来说，“Q&R”(质量和监管)部门包括营销和 R&D(研发)部门。以我们的 Chest 为例，考虑一个团队，其中有详细了解业务领域的产品经理、软件工程师、测试人员和数据科学家。

![](img/ba4702b2fe7b0afbe8a5499e2d91de6d.png)

如果您将数据科学家视为人工智能项目经理，则该角色包括领导与监管机构的沟通，以获得官方批准(例如，对于美国:强制性 FDA 510(k)流程)和 FDA 或 tüV 等机构的官方审计(在欧洲，根据 MDR)。

在这种情况下，数据科学家能够解释软件工程过程以及技术人工智能基础知识、人工智能产品软件的关键组件及其以一般可理解的方式进行解释是至关重要的。Q&R 和监管机构的员工通常没有必要的工程背景来进行人工智能讨论，这也不是他们的工作。他们主要关注的是监管和投诉，而不是人工智能算法的数学深度。

例如，为了更好地了解 CNN 在其隐藏层内部正在做什么，[迪潘然(DJ)萨卡尔](https://medium.com/@dipanzan.sarkar?source=post_page-----f95683e23c1d----------------------)在他的博客[帖子](https://medium.com/google-developer-experts/interpreting-deep-learning-models-for-computer-vision-f95683e23c1d)中为 CNN 介绍了一些关于解读深度学习模型的**解读技巧**。例如,*使用 GradCAM，我们通过查看类激活图(CAM)来尝试并可视化图像的部分如何影响神经网络的输出。*"您可以识别并可视化特定隐藏层块聚焦在图像的哪个区域。

![](img/8310c2014da97a72370358dd9fed31ff.png)

像在这个猫的例子中，聚焦在第一个隐藏层(顶部)的边缘和角落；在较高的隐藏层(底部),关注周围环境和面部结构。*’*可解释 AI([](/human-interpretable-machine-learning-part-1-the-need-and-importance-of-model-interpretation-2ed758f5f476)**)‘对于医学领域的数据科学家来说，是一个很好了解的自己的研究领域。**

**除了解释之外，监管机构还会立即提出进一步的问题:**

*   ***是否已经有可用的解决方案？那里用的是什么样的数据？我们可以与之比较的其他解决方案的指标评估是什么，或者是否有“官方”指标值？*细胞杂志[论文](https://www.cell.com/action/showPdf?pii=S0092-8674(18)30154-5)“通过基于图像的深度学习识别医学诊断和可治疗疾病”中描述了一种已经存在的解决方案。在德国举行的人工智能医学研讨会上(2019 年 7 月)，tüV 的一名代表提到 86%的测试准确率是这项医学分类任务的参考性能值。**

**数据科学家必须解释评估指标，因为这是一个医疗诊断问题，例如混淆矩阵的假负值(2 型错误)对于选择正确的模型也非常重要。对于患有肺炎的儿童，CNN 模型结果的高假阴性值导致他们生病，但软件认为他们是健康的，生病的儿童不会得到所需的必要医疗护理。**

**关于我们使用数据集**V3 60–20–20:**的模型实现，如果决定使用具有最高测试准确性的模型，那么选择具有 Adam 优化器和增强的基本模型:其值为 89.33%。但是 is 已经检测出 57 个漏报，太多了。如果决定在最低数量的假阴性上具有更高的 prio，则具有 Adam 优化器和瓶颈功能的 ResNet50 转移模型是最终模型——只有 5 个假阴性，测试准确度为 84.80%。**

# ****结论****

**人工智能算法有可能改变未来常见的医疗工作流程([来源](https://www.healthcatalyst.com/prescriptive-analytics-improving-health-care))。**

**为了开发和营销合格的医疗人工智能产品，公司结构和管理思维需要改变。对于数据科学，软件工程需要更高的认可地位和合适的合格员工。和监管方面需要高素质的数据科学家沟通技巧。**

**关于我们的例子，目标是减少五岁以下儿童死亡总数的 15%，对于我们的编码及其最终软件解决方案(使用瓶颈特性的 RestNet50 转移模型 **)** ，所使用的模型超参数被认为是起点**。期望进行详细的超参数调整，以获得更好、稳定的预测和度量结果(例如，测试准确度> 86%，假阴性数量低(< 5))。此外，获得更好结果的更高级的隐藏层结构和隐藏层的解释概念还没有实现。它的计算成本很高，并且需要合适的硬件环境。****

****[1]将 Kaggle 数据集的胸部图像、[医疗 youtube 视频](https://www.youtube.com/watch?v=HNGNQMhsxx4)和 databricks 论文“人工智能民主化和深度学习”的图表组合起来，创建自己的图表****

****[2] SAP 课程“数据科学入门”****