# 人工智能:可以用任何语言解释

> 原文：<https://towardsdatascience.com/artificial-intelligence-explainable-in-every-language-4fbdf2dd0b27?source=collection_archive---------32----------------------->

![](img/8b3e03a1fa10e0783e0a65782244aa5f.png)

**什么是 Ai？**
这要看你问谁了。当这个术语在 1956 年被创造出来的时候，“人工智能”已经忍受了一生的误解。

可解释性是缺失的一环，也是它被误解的原因。问题出在对“智力”这个词的解释上。用传奇计算机科学家 Edsger Dijkstra 的话说:“计算机能否思考的问题并不比潜艇能否游泳的问题更有趣。

如果我问你谁是更好的游泳运动员，你会选择迈克尔·菲尔普斯还是伊利诺斯号？游泳是人的活动，当然不是潜艇做的事。然而，潜水艇游得比任何游泳者都快得多，距离也远得多。

智力就像游泳；我们把它和生物联系在一起。更令人困惑的是，人类长期以来一直在“转移目标”智力的构成要素。1642 年，帕斯卡写道，一个设备“最终将在不依赖人类智能的情况下完成所有四种算术运算。”看起来，帕斯卡会把加、减、乘、除的能力看作是智能，而在计算器上这样做的能力会是人工(机器)智能的一种形式。快进到今天，计算器被认为是最基本的。问题就在这里:通过承诺智能，人工智能设置了一个高的、模糊定义的障碍，破坏了它实际上可以和已经实现的一切。

人工智能通常至少展示了以下一些与人类智能相关的行为:规划、学习、推理、解决问题、知识表示、感知、运动和操纵，以及在较小程度上的社会智能和创造力。

**Ai 类型**
高级 Ai 可以分为两大类:狭义 Ai 和广义 Ai。

> 狭义人工智能是我们今天在计算机中看到的一切:智能系统已经被教会或学会如何执行特定的任务，而没有被明确编程如何这样做。

这种类型的机器智能在 iPhone 上苹果 Siri 虚拟助手的语音和语言识别中，在自动驾驶汽车的视觉识别系统中，在根据你过去购买的东西推荐你可能喜欢的产品的推荐引擎中，都很明显。与人类不同，这些系统只能学习或被教会如何完成特定的任务，这就是为什么它们被称为狭义 Ai。

> 通用人工智能非常不同，它是在人类中发现的适应性智力类型，是一种灵活的智能形式，能够学习如何执行完全不同的任务，从理发到建立电子表格，或者根据积累的经验推理各种各样的主题。这是一种在电影中更常见的人工智能，像 2001 年的哈尔或终结者中的天网，但今天并不存在，人工智能专家对它多久会成为现实存在激烈的分歧。

人工智能研究人员文森特·C·穆勒和哲学家尼克·博斯特罗姆在 2012/13 年对四组专家进行的一项调查报告称，2040 年至 2050 年间，AGI(人工通用智能)有 50%的可能性被开发出来，到 2075 年这一比例将升至 90%。该小组甚至更进一步，预测所谓的“超级智能”——博斯特罗姆将其定义为“在几乎所有感兴趣的领域中大大超过人类认知表现的任何智力”——预计将在 AGI 成就约 30 年后出现。尽管如此，一些人工智能专家认为，鉴于我们对人脑的了解有限，这种预测过于乐观，并认为 AGI 仍有很长的路要走。

**是什么推动了人工智能的复兴？**
近年来人工智能研究的最大突破是在机器学习领域，尤其是深度学习领域。这在一定程度上是由数据的易获得性推动的，但更重要的是由最近并行计算能力的爆炸推动的，在此期间，使用 GPU 集群来训练机器学习模型变得更加普遍。

这些集群不仅为训练机器学习系统提供了强大得多的系统，而且它们现在可以作为互联网上的云服务广泛使用。主要的科技公司，如亚马逊、谷歌和微软，已经开始使用专门为运行和最近的训练机器学习模型量身定制的处理器。

这些定制处理器的一个例子是谷歌的张量处理单元(TPU)，其最新版本加快了使用谷歌 TensorFlow 软件库建立的机器学习模型从数据中推断信息的速度，以及它们可以被训练的速度。

这些处理器不仅用于训练 DeepMind 和谷歌大脑的模型，还用于支撑谷歌翻译和谷歌照片中的图像识别的模型，以及允许公众使用谷歌的 TensorFlow 研究云建立机器学习模型的服务。第二代处理器在两年前的 5 月份谷歌 I/O 大会上亮相，这些新的 TPU 阵列能够训练用于翻译的谷歌机器学习模型，时间是高端图形处理单元(GPU)阵列的一半。

**什么是机器学习？**

机器学习(ML)是对算法和统计模型的科学研究，计算机系统使用这些算法和统计模型来执行特定任务，而不使用显式指令，而是依赖模式和推理。它被视为人工智能的一个子集。

简而言之，ML 用数据来回答具体问题。今天，享受某种复兴，ML 是计算机系统被输入大量数据的地方，然后它使用这些数据来学习如何执行特定的任务，例如理解语音或为照片添加字幕。

**ML 有哪些要素？**
一般来说，ML 可以分为两大类:有监督的和无监督的学习。

> 有监督的学习
> 教授人工智能系统的一种常见技术是通过使用大量带标签的例子来训练它们。这些模型被输入了大量的数据，这些数据被注释以突出感兴趣的特征。这些可能是贴有标签的照片，以表明它们是否包含一只狗，或者是有脚注的书面句子，以表明“bass”一词是与音乐还是鱼有关。一旦经过训练，模型就可以将这些标签应用于新数据，例如刚刚上传的照片中的一只狗。

这种通过例子来教授模型的过程被称为监督学习，标记这些例子的角色通常由在线工人来完成，他们通过亚马逊机械土耳其公司这样的平台来雇佣。

训练这些模型通常需要大量数据，一些模型需要搜索数百万个例子，以学习如何有效地执行任务——尽管在大数据和广泛数据挖掘的时代，这越来越有可能。训练数据集非常庞大，而且规模还在不断增长——谷歌的开放图像数据集约有 900 万张图像，而其标记的视频库 YouTube-8M 链接到 700 万个标记的视频。ImageNet 是这种类型的早期数据库之一，拥有超过 1400 万张分类图像。历时两年，由近 5 万人(其中大部分是通过亚马逊土耳其机械公司招募的)整理而成，他们检查、分类并标记了近 10 亿张候选照片。

从长远来看，访问巨大的标记数据集也可能不如访问大量计算能力重要。最近，GANs(生成对抗网络)展示了被输入少量标记数据的 ML 系统如何产生大量新数据来自学。

这种方法可能会导致半监督学习的兴起，在这种学习中，系统可以学习如何使用比今天使用监督学习的训练系统所需的更少量的标记数据来执行任务。

> **无监督学习**
> 相比之下，无监督学习使用了一种不同的方法，算法试图识别数据中的模式，寻找可以用来对数据进行分类的相似性。

例如，将重量相似的水果或发动机大小相似的汽车聚集在一起。

该算法并没有预先设置来挑选特定类型的数据，它只是寻找可以根据其相似性进行分组的数据，例如，谷歌新闻每天将类似主题的故事分组在一起。

> **强化学习**
> 强化学习的一个粗略类比是当宠物表演一个把戏时奖励它一份食物。

在强化学习中，系统试图根据其输入数据最大化奖励，基本上经历一个试错过程，直到达到最佳可能结果。

强化学习的一个例子是谷歌 DeepMind 的 Deep Q-network，它在各种经典视频游戏中的表现超过了人类。该系统从每个游戏中获取像素，并确定各种信息，例如屏幕上物体之间的距离。

通过查看每场比赛中获得的分数，系统建立了一个模型，该模型显示在不同情况下哪个动作将使分数最大化，例如，在视频游戏“突围”的情况下，为了截住球，应该移动球拍。

**什么是神经网络？**

机器学习过程的关键是神经网络。这些是大脑启发的算法互连层网络，称为神经元，它们将数据输入彼此，并可以通过修改输入数据在层间传递时的重要性来训练它们执行特定任务。在这些神经网络的训练过程中，附加到不同输入的权重将继续变化，直到神经网络的输出非常接近所期望的，此时网络将已经“学会”如何执行特定的任务。

机器学习的一个子集是深度学习，其中神经网络被扩展为具有大量层的庞大网络，这些层使用大量数据进行训练。正是这些深度神经网络推动了计算机执行语音识别和计算机视觉等任务的能力的飞跃。

有各种类型的神经网络，具有不同的优点和缺点。RNNs(递归神经网络)是一种特别适合于语言处理和语音识别的神经网络，而 CNN(卷积神经网络)更常用于图像识别。神经网络的设计也在不断发展，研究人员最近改进了一种更有效的深度神经网络形式，称为 LSTM(长短期记忆)，使其运行速度足够快，可用于谷歌翻译等按需系统。

人工智能研究的另一个领域是进化计算，它借鉴了达尔文著名的自然选择理论，看到遗传算法在世代之间进行随机突变和组合，试图进化出给定问题的最优解。

这种方法甚至被用来帮助设计人工智能代理，有效地使用人工智能来帮助构建人工智能。这种使用进化算法优化神经网络的方法被称为神经进化，随着智能系统的使用变得更加普遍，特别是在数据科学家的需求经常超过供应的情况下，它可能在帮助设计高效人工智能方面发挥重要作用。这项技术最近由优步人工智能实验室展示，该实验室发布了关于使用遗传算法来训练深度神经网络以解决强化学习问题的论文。

最后，还有专家系统，其中设备被编程有规则，允许它们基于大量输入做出一系列决定，允许机器模仿特定领域的人类专家的行为。这些基于知识的系统的一个例子可能是，例如，驾驶飞机的自动驾驶系统。

## 人工智能将如何影响我们的世界？

> 自动驾驶汽车和机器人
> 对机器人能够自主行动、理解和导航周围世界的渴望意味着机器人和人工智能之间有天然的重叠。虽然人工智能只是机器人技术中使用的技术之一，但人工智能的使用正在帮助机器人进入新的领域，如自动驾驶汽车、送货无人机，以及帮助机器人学习新技能。通用汽车(General Motors)最近表示，将在 2019 年前制造出没有方向盘或踏板的无人驾驶汽车，而福特承诺在 2021 年前做到这一点，谷歌母公司 Alphabet 内部的自动驾驶集团 Waymo 将很快在凤凰城提供无人驾驶出租车服务。
> 
> **假新闻**
> 我们即将拥有能够创造照片般逼真的图像或以近乎完美的方式复制某人声音的神经网络。随之而来的是巨大的破坏性社会变革的可能性，比如不再相信视频或音频片段是真实的。人们也开始担心这些技术将如何被用来歪曲人们的形象，因为已经有工具被用来令人信服地拼接著名女演员。
> 
> 语音和语言识别
> 机器学习帮助设备识别人们在说什么，准确率接近 95%。最近，微软的人工智能和研究小组报告说，他们已经开发出一种系统，能够像人类转录员一样准确地转录英语口语。随着研究人员追求 99%的准确率，预计对设备说话将与更传统的人机交互形式一起成为常态。
> 
> **面部识别和监控**
> 如今，面部识别系统的准确性已经向前迈进了一大步，中国科技巨头百度表示，只要视频中的人脸足够清晰，它就可以以 99%的准确率匹配人脸。而西方国家的警察部队通常只在大型活动中试用面部识别系统。在中国，当局正在启动一项全国范围的计划，将全国各地的闭路电视连接到面部识别系统，并使用人工智能系统跟踪嫌疑人和可疑行为，同时也在测试警方使用面部识别眼镜。尽管世界各地的隐私法规各不相同，但这种对人工智能技术的更具侵入性的使用——包括可以识别情绪的人工智能——很可能会在其他地方逐渐变得更加普遍。
> 
> 人工智能可以对医疗保健产生巨大影响，帮助放射科医生在 x 射线中挑出肿瘤，帮助研究人员发现与疾病有关的基因序列，并识别可能导致更有效药物的分子。世界各地的医院都在进行人工智能相关技术的试验。其中包括 IBM 的沃森临床决策支持工具，该工具由纪念斯隆-凯特琳癌症中心的肿瘤学家培训，以及英国国家医疗服务系统对谷歌 DeepMind 系统的使用，该系统将有助于发现眼部异常，并简化筛查头颈癌患者的过程。

结论
人工智能有可能颠覆许多行业，其商业模式基于利用算法，从推荐引擎和商业分析到医疗诊断和自动驾驶汽车，但我们希望从一开始就确保以负责任和道德的方式完成这项工作。