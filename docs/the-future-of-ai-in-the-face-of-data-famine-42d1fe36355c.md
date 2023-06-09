# 面对数据饥荒的人工智能的未来

> 原文：<https://towardsdatascience.com/the-future-of-ai-in-the-face-of-data-famine-42d1fe36355c?source=collection_archive---------23----------------------->

![](img/40e1c20f44a9c0cb6917791497de1c76.png)

Photo by [Mathew MacQuarrie](https://unsplash.com/@deskfire?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/death?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

人工智能研究领域作为一门学术学科创建于 1956 年。尽管有 60 年的历史，但这个时代仍处于最开始，与类似学科相比，未来的道路崎岖不平，这主要是由伦理和数据可用性领域的挑战驱动的。

**AI 的命运起伏** 人工智能自诞生以来，经历了三次重大突破和两次停滞期。它最近的复兴是在 2016 年引发的，当时 AlphaGo 击败了世界上最好的围棋选手，这是一场被认为对人工智能来说太复杂的游戏。

正如我们从以前的人工智能圈子中了解到的那样，每当它向前迈出一大步，就会有很多人审视和关注这对世界意味着什么；无论是行业还是社会。因此，人工智能的某些想法在公众中变得极具争议，并进入了“幻想破灭的低谷”。

思考一下为什么人工智能仍然如此有争议，事实证明，对人工智能能够提供什么的期望与它在现实中能够完成什么之间存在巨大差距。今天的事实是，人工智能的真实世界例子仍然很少，而且往往专注于非常小众的案例，远离营销人员撰写的追逐社交点击的场景。AI 走向主流还有很长的路要走。由于我们在这个领域并不缺乏远见，我们看到了对人工智能今天真正能够完成什么的怀疑信号。现在，在第三次人工智能崛起即将结束之际，这个新兴领域的命运仍不确定。

**数据饥荒即将来临** 人工智能最近的崛起在很大程度上是由大数据的可用性推动的，大数据推动了面部识别等领域深度学习的发展，这可以被认为是这场人工智能浪潮的主要突破之一。在更复杂的领域，如疾病诊断，深度学习仍然面临着弥合企业和机构之间差距的挑战。这一领域的一个主要问题是数据的可访问性。从整体的角度来看，数据是可用的，但由于若干原因是不可评估的。一个常见的问题是数据存储在孤岛中。这些孤岛通常是公司内部网络甚至公司内部物理隔离的结果。另一个突出的问题是数据结构不兼容。因此，没有集中式数据中心来通过深度学习机制训练强大的神经网络。基于云的计算经常被认为是解决数据孤岛问题的潜在解决方案，但事实证明，对于大量数据来说，它既昂贵又耗时。此外，还有越来越严格的数据隐私法规，如通用数据保护法规。虽然这些政策对于保护消费者的隐私非常重要，但它们也对数据的使用施加了严格的限制，并要求重新思考如何以合规的方式构建人工智能应用。

**联合学习——第四大突破的承诺** 消费者保护实践和数据隐私是不可协商的，也是建立必要信任的底线。另一方面，它带来了数据饥荒和人工智能崛起放缓的风险。联邦学习是一种新的人工智能方法，有可能带来人工智能的下一个重大突破，并克服这一波数据隐私和信任挑战。它是一个机器学习框架，允许用户使用分布在多个位置的多个数据集来训练机器学习模型，同时防止数据泄露并遵守严格的数据隐私法规。实际上，根据数据的分布特征，联合学习有三个主要类别。

水平联合学习根据特征划分数据集，并且通常在特征重叠多于用户的情况下实施。例如，在不同地区运营的三家物流公司可能会保留其消费者的类似数据，但消费者本身之间的重叠相对较小。由于他们的特征几乎相同，因此可以提取具有相同特征的用户来训练模型。

当多个数据集具有大量重叠的用户但具有不同的特征时，通常使用垂直联合学习。例如，在同一地区经营的食品配送服务和医院可能有一组相似的用户，但跟踪两者之间的不同信息:医院跟踪健康数据，而食品配送服务跟踪浏览习惯和购买数据等。垂直联合学习集合了所有这些特征，以便为双方协作建立一个模型。

当数据集的用户和特征之间几乎没有重叠时，联合迁移学习用于克服这种数据或标签的缺乏。以中国的一家制造商和美国的一家物流供应商为例。由于它们在地理上受到限制，用户之间很少有重叠；同样，由于它们是不同类型的机构，它们的特征也很少重叠。在这种情况下，迁移学习应该与联合学习结合使用，以定义数据集之间的通用表示，并提高模型的整体性能。

尽管它有能力，但仅靠一个有效的框架不足以完全解决这些挑战。联合学习必须发展成为一种商业应用，为某个行业提供灵活、双赢的商业模式。通过聚合不同机构的多个孤立数据集，联合学习使开发理想模型成为可能，而无需侵犯每个人的隐私。简而言之，这是一种通过将来自多个利益相关者的数据保存在孤岛中来训练算法的方法——数据共享经济，其中数据持有者通过共享他们的数据而受益，而应用程序提供商可以通过提供开发这些模型所需的服务来获利。

由...所写

西哈诺·陈、锡安·陈和迈克尔·伦茨