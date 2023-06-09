# 用数字工具绘制知识图谱，解决 21 世纪的医疗保健问题

> 原文：<https://towardsdatascience.com/mapping-knowledge-with-digital-tools-to-solve-healthcare-problems-in-the-21st-century-21a19a51c81d?source=collection_archive---------13----------------------->

## ***托普塔尔奖学金赋能未来女性领导者的论文***

# 介绍

当我在医学、学术研究和生物技术领域旅行时，我清楚地认识到，从业者和研究人员正在努力应对我们今天面临的复杂的健康挑战。这些健康问题需要超越生理学和生物化学的理解，因为疾病还受到社会和文化的影响。此外，我们还生活在一个以不断变化的气候和生物多样性丧失所加剧的新情况为特征的时代，当涉及到对人类健康的影响时，我们仍然难以完全理解这些因素。

![](img/c1881b7da29eb2416e91fb52e13bf890.png)

The effects of climate change and loss of biodiversity on human health cannot be understood by reductionist scientific enquiry alone.

在理想的世界中，我们创造的知识和解决方案应该足以解决这些复杂的问题。不幸的是，纯粹的信息过载使获得一个概览成为一项艰巨的任务，导致大多数研究人员退缩到专业的筒仓中，从职业的角度来看，这些筒仓更容易管理，也更安全。

所有这一切让我意识到，我们今天面临的复杂的健康挑战无法通过当前推动医疗保健研究和知识创造的过程来解决。如果我们要创造持久的解决方案，作为研究人员，我们必须理解更大的图景，获得当今时代导致疾病的许多观点的概述，并将这些观点纳入我们的研究。

在寻找工具和方法来整合健康问题固有的不同观点的过程中，我继续探索远离科学和医学舒适区的领域。第一个是设计思维，或以人为中心的设计。作为斯坦福大学设计研究中心的访问学者，我每天都在学习设计师如何解决问题，并参与了许多设计项目。这一经历让我意识到使用设计方法探索复杂问题空间和以不同方式构建问题的可能性。

虽然设计方法对于创建医疗保健实际挑战的解决方案，甚至帮助组织转型非常有用，但我仍然缺乏获得研究信息概览的方法，而这对于开始更下游的设计过程是必要的。在这种需求的驱动下，我开始冒险进入另一个远远超出我最初专业知识的领域，一个将我带入算法和网络世界的领域。

# **测绘知识**

众所周知，人类大脑处理视觉信息的效率远远高于书面信息，这种现象与大脑同时处理多个视觉信息的能力有关，而不是一次处理一个单词。尽管如此，大多数科学出版物和数据库都严重依赖书面信息。由于无法可视化，研究人员只能在长长的出版物列表中滚动，无法立即获得某个领域的概况。事实上，我遇到的大多数研究人员除了偶尔在一篇研究文章上乱涂乱画，然后存档，再也不会被看一眼之外，没有任何可视化的方法来跟踪他们领域的研究。一些新的 web 应用程序(如 Dimensions 和 Meta)稍微改进了这一过程，尽管数据仍然以长列表的形式呈现，而不是可视化。

在与一位从事图形数据库和网络工作的数据科学家讨论后，我偶然发现了映射的概念。从那里，我发现从事分析科学本身的个人，如科学计量学和科学知识社会学的人，一直在使用机器学习和数据提取技术的工具来绘制知识的演变。尽管如此，在这些专门的亚群体之外，很少有人敢于超越理论领域，将他们的发现付诸实际应用，这使得大多数研究人员、从业人员和政策制定者不太重视这些发现。这可能是解释为什么那些研究科学的人和那些实际实践科学的人之间很少交谈的一个原因。

与数据科学家一起，我们开始探索绘制结核病领域的地图，以找出这种方法可以带来什么。在这个过程中，我们发现许多免费工具要么太复杂，非数据科学家无法使用，要么缺乏复杂性，无法回答我们感兴趣的问题。通过我们的探索，我们开始开发自己的工具，使我们能够直观地浏览网络，并以有趣和创造性的方式处理数据。

将知识网络可视化使我能够从数据中获得洞察力，这在以前是不可能的。例如，使用我们新创建的工具来探索结核病领域的引用网络，很明显该领域正在朝着一个非常独特的方向发展，随着时间的推移，明确的研究领域被放弃。随着调查的深入，废弃区域被发现为结核病诊断区，由于该领域资金缺口巨大，世卫组织最近将该领域确定为优先领域。我们创建的可视化使我们能够在概览中看到这一差距，而无需手动梳理大量文献，我们相信这可以以更有效的方式促进决策者的战略进程。这种类型的分析也与研究人员相关，他们可能能够在更大的领域背景下可视化他们的研究，甚至识别最近被遗忘的潜在有趣的研究，如在[中看到的这个例子](https://anivation.wordpress.com/2018/08/06/the-overlap-between-infectious-diseases-and-chronic-illnesses/)。

![](img/b1221667128dc1b2392a09e424e7bc05.png)

A static screenshot of the interactive citation network using the tool we developed. The program allows users to scroll over each node (research article) and obtain details as well as visualize its direct connections within the network. The network can be seen to have a shape, which tells us that as new articles are published, older ones are no longer being cited. We can observe a clear area that had been thinning out over time, which in this case, corresponded to articles discussing TB diagnostics.

从那时起，通过使用我们的工具，我分析了合作网络中的模式，揭示了学术界和工业界之间的不同合作动态，以及目前处于边缘地位但代表未开发潜力的新兴研究领域。

![](img/f8d3f949d7b69a37bf6f797d3a031114.png)

Analyzing collaboration networks revealed clearly the disconnect between industry and academia in the field of multi-drug resistant tuberculosis. Here, a small cluster involving Johnson and Johnson’s pharmaceutical arm, Janssen Pharmaceuticals can be seen to be disconnected from the main research network.

为了理解围绕健康话题的更广泛的背景，我还[分析了围绕结核病和全球健康话题的 twitter 网络](https://anivation.wordpress.com/2018/09/26/discourse-analysis-of-the-twitter-hashtag-unhlmtb/)，它提供了围绕这些主题的生态系统和观点的广泛概述。

![](img/84d80b7a43ffcf8923316d69953c9fe3.png)

Examining a twitter network reveals the ideas that are spreading and how they are inter-connected within a health topic, in this case, global health. It gives us an idea about the discourse, or the issues that are important in the community; knowledge that cannot be gathered from official research articles.

随着时间的推移，通过这项工作，一个愿景开始出现，一个我觉得令人兴奋且深具意义的愿景。重要的是，我认为这是一个愿景，它解决了知识创造和利用方式中的一个主要差距，因此可能具有深远的潜力，以我们尚未完全预见的方式转变科学进步并造福社会。

# 视力

你是一名研究人员，需要决定你的下一个调查，以便写下你将要申请的资助。或者，你可能是一个政策制定者，他需要决定是否有更多的钱需要分配给某个特定的领域。你也可以是一名设计师，与当地的流行病学家一起工作，寻求建立一个更好的系统来识别传染病爆发的源头。

在每一种情况下，你的下一步将取决于你对你将要从事的领域的理解和综合能力。这一过程通常需要几个小时、几周甚至几个月的时间来研究这个主题，以便对这个主题的所有可能的角度有一个全面的了解。

![](img/50ad6aff8a9b62ea51851da8f21cdbd6.png)

Fancy reading through these articles anyone?

现在想象一下另一个现实，点击几下鼠标，你会发现自己在浏览你感兴趣的主题的交互式视觉概览。然后，你迅速确定差距和追求的机会，引导你创建一个合理的和原创的战略或研究方向。当需要时，你现在可以将你更深入的研究锁定在一个非常具体的领域，而不必浪费无数的时间去挖掘不相关的信息。最重要的是，你意识到这是如此有趣，以至于你不断探索，直到你偶然发现一个有趣的见解，让你问了一个你以前从未想过的问题。顺便说一句，这个问题导致了改变生活的疗法或神奇产品的发展，它改变了整个社会人们的健康状况。

如果这个愿景让你兴奋，那么我会说这不是一个遥远未来的愿景。使这成为现实的工具和技术已经存在，而我今天的任务，就是把它引入你们的世界，并为了更大的利益改变我们利用知识的方式。

![](img/e544d823f8cd08892a0ae5b7b7a5d197.png)

Data sources that can be used will originate from diverse sources and will be subjected to the same processing to create infoscapes that allow the investigator to play with the visualizations and extract insights.

# 履行

我们的工具目前处于开发的最后阶段，我们预计我们将能够在年内公开这一点。作为一名非技术(数据科学家)联合创始人，我的职责是在数据科学和医疗保健研究之间架起一座桥梁。为了做到这一点，我打算与该领域的专家建立合作关系，并用现实世界的问题创建用户研究。潜在的合作者已经确定，项目将在未来几个月启动。用户研究对于获得重要反馈至关重要，它将使我们能够进一步改进产品。

仅仅开发一个数字工具是不够的，而不开发使用它的技术。因此，我致力于开发一种方法，允许对数据进行更系统的调查。从这项工作中获得的一些见解可以在这里看到[。在接下来的几个月里，我将继续研究这种方法，并对其进行微调，以创建一个完整的框架，供用户在探索数据时参考。](http://www.anivation.org)

由于我们目前自筹资金，没有外部资金来源，下一步将是积极寻求和确保进一步开发该工具的资金。用户研究将是我们吸引合作伙伴或投资者能力的重要组成部分。尽管我们已经制定了业务计划，确定了增长潜力，并将我们的工具与潜在的竞争对手区分开来，但该计划需要进一步完善，才能更有影响力。

需要明确的是，这个项目的目标不是简单地启动一个创业公司来推广一个产品。该项目旨在通过确保有价值的知识不会迷失在信息的海洋中，确保社会从多年的科学研究中获得最大收益。因此，可能还有其他途径有待探索，以使这一愿景成为现实。

例如，这可能是一个咨询服务的路线，该服务将与产品一起提供，由我领导，以确保用户从使用该工具中获得最大利益。

# 成为女性领导者

2018 年，我参加了在巴塞罗那举行的 EIT Health 增强女性在健康创新方面的领导力研讨会。在这次研讨会期间，我意识到女企业家在企业家世界中的代表性不足的程度。我还了解到，有抱负的女性企业家应该寻求的最重要的东西之一是导师，而这正是我目前努力的方向。

使 [Toptal 的提议](https://www.toptal.com/scholarships-for-women?fbclid=IwAR2sozmtpcLZvOJaXDkpDUwLK9PXqJzTEIgeD9kAPUjaOJRhzj1yapOxe9I)特别相关的是它提供的指导支持。我认为，导师不仅仅是传授技术建议，对我来说更重要的是，它是从以前走过这条路的其他人的经验中学习。我理想的导师是一位探索过不同职业道路的女性领导者，从与企业合作到创办自己的企业或咨询公司。独立工作意味着大部分时间要么花在自己身上，要么花在与其他团队成员讨论上，这导致获得外部意见的机会很少。在我职业生涯的这一关键时刻，与导师进行定期讨论不仅能鼓舞士气，还能极大地增强我的观点和视野，并拓宽我的视野，让我能通过其他途径将这一愿景变为现实。

改变世界是一项艰巨的任务，单靠自己是无法完成的。只要有一点帮助，这个想法的种子就可以发芽，形成一个复杂的连接网络来维持它，并开花成为一棵宏伟的树。

![](img/5e63d6361e850c0407a733aa427f0840.png)

The tree of knowledge :)