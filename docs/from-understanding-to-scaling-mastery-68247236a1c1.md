# 从理解到掌握。数据专业人员面临的问题类型以及如何应对

> 原文：<https://towardsdatascience.com/from-understanding-to-scaling-mastery-68247236a1c1?source=collection_archive---------47----------------------->

![](img/61e30230ea0313c900f15523cf1cf163.png)

当你开始一个新的数据科学或分析角色时，你做的第一件事是什么？你知道，除了安装你需要的所有必要的工具和软件包，以及访问数据？如果你还没有，明智的做法是做一个*数据问题审计，*找出你的组织中数据可以发挥作用的所有领域。

数据问题审计是简单地进行一系列的访谈，以暴露组织中存在的问题，这些问题可以用数据来回答。无论您是个人、团队领导，甚至是受托开发数据战略的人，提出所有这些问题都是有价值的。根据我做上述所有事情的经验，经常会出现四类问题。

它们是:

**一级分析(了解)**

> 告诉我<x>的价值</x>

**二级分析(理解)**

> 不要只报告趋势，告诉我为什么会这样

**三级分析(掌握)**

> 我喜欢这些趋势，但是我们能全面彻底地回答<y>吗？</y>

**第 4 层分析(扩展精通)**

> 我喜欢你迄今为止所做的一切，我们能不能把你从等式中去掉，建立一些永久有效的东西

第 1 级问题的一个例子是，如果您被问到实际值和目标值之间的差值是多少。分析师应该用不到一天的时间来回答这些问题。应对这些问题的主要技能是数据挖掘和开发可视化的能力。

第二层是，如果你被要求调查造成这种差异的因素。根据问题的复杂程度，回答这个问题可能需要几个小时，甚至几天。

第三层是要求你全面回答实际和目标之间的关系是什么，它是如何随着时间的推移而演变的，以及有哪些因素影响它。这样做的时间通常会超过一周。第 2 层和第 3 层需要结合数据挖掘、分析和数据科学专业知识。

第 4 层是当您被要求开发一个模型来预测一个值或结果时(在某些情况下，您最初被要求简单地报告的那个，在我们的例子中是“实际值”)。这需要 ML 模型的生产、测试和部署，可能需要几个月的时间。这是数据科学的领域，也是数据工程师的领域。

> *从简单地报告正在发生的事情，到预测性分析解决方案的部署和扩展，这个连续体将带您了解一切。从了解到掌握。那么现在你的审计已经告诉你那里有什么，你会怎么做呢？*

# 自动化简单的事情

你的第一级问题是 BAU 问题，没有上下文。在这些问题中，您的利益相关者可能只需要知道一个数据点，而不需要深究它的实际含义。

这些任务通常落在分析团队身上，尽管他们中的一些人可能仍然留在商业领域(尽管这两者应该保持同步)。鉴于许多组织刚刚开始投资和建立他们的分析和数据科学团队，你可能会对你的审计中属于这一领域的问题的比例感到惊讶。如果您已经加入了一个新生的数据功能，或者正在一个初创的环境中工作，这一点尤其正确。您的组织已经承诺构建数据能力，他们可能有大量积压的项目需要分析团队来处理，其中许多项目都在这一流程中。

虽然这些之前积压的问题可能会得到很好的回答，而且它们相对容易解决，但它们本身会带来一些风险，你需要减轻这些风险。它们包括:

1.  分析师流失的风险:没有多少分析师只是在游戏中挖掘数据点——他们希望产生影响，并使用他们的技能来弄清事情的真相。此外，由于这些查询的 BAU 性质，未能自动化您的第 1 级响应可能会导致任务重复
2.  没有得到重要东西的风险:记住*知道*是走向*掌握*的连续体的开始。你需要把简单的事情处理掉，让你开始真正的增值任务
3.  预期与现实不符的风险:数据资源并不便宜。如果你没有管理预期，并且一直在解决 BAU /低附加值问题，这可能会对组织从数据中获得(或认为获得)多少价值产生影响

> *幸运的是，你解决第一层问题的方法很简单。一旦你确定了这些问题，你就可以腾出时间自动给出他们的回答。*

这通常通过开发自助仪表盘来实现。花几个月的时间开发一个自动化的自助服务解决方案，满足您的组织的所有第 1 层报告需求，并让您的团队有时间从事更高附加值的工作。更好的是，如果你做得好，这将在可预见的未来解决这些问题，只有当企业进入新的垂直市场或获得新的(重要的)数据源时，才需要扩展。它还将作为第 2 级和第 3 级问题的线索和来源，您将需要花大部分时间来解决这些问题。

# 第二层和第三层是你的面包涂黄油的地方

您在自动化第 1 级响应方面所做的所有出色工作都是为了腾出时间，以便您和您的团队能够在这个领域开展工作。这些都是很有价值的问题。此外，随着你的组织开始使用更多的数据，他们将有一个定期和有机的需求流，并要求你调查每当你回答第 1 级问题时出现的趋势。第 2 级和第 3 级非常相似，主要区别在于回答每个问题所需的时间，以及回答问题的结论性。

例如，第 2 层的问题可能是:“我们想调查为什么销售额逐年下降”，而第 3 层的问题可能是“我们想了解是什么因素推动了销售，以及我们如何能够销售更多的产品”。前者更局限于特定的场景，而后者更开放，更有结论性，需要你穷尽所有可能的调查途径。

> *另一个区别是，第 2 级问题可能用于告知战略行动，而第 3 级问题可能告知战略方向(或某些战略行动将级联的总体战略)。一个放入 powerpoint，另一个放入纸板。*

重要的是要认识到这两个领域的重要性，并管理期望，以便您将 80%的时间花在这两个领域上(当然是自动回复第 1 级问题)。你还应该积极主动地确定你的组织可能想要全面回答的领域(第 3 级)，并开始抽出时间来解决这些问题，因为它们可能需要几周或几个月的时间来全面回答。

> *这些是你将会花大部分时间去解决的问题，所以花点时间来构建你的团队工作流程和节奏，以公正地对待它们。*

# 规模重要性

现在你已经自动回答了最简单的问题，并且开发了一个很好的节奏让你去做最重要的事情，那么剩下的是什么呢？最后一个阶段是确定您的组织希望在未来和永久得到回答的问题，即第 4 层。这一步要求您自动回答复杂的问题，您是否能够在处理重要的组织问题时，生成能够提供足够准确性的模型或工具？本质上，这需要预测模型的产生和部署，甚至可能是全面的数据工程。

这里的挑战是识别 a)存在的和 b)需要优先考虑的用例，假设你每年只执行几个用例( [if that](https://www.mckinsey.com/business-functions/mckinsey-analytics/our-insights/the-executives-ai-playbook?page=value/align/) )。从优先顺序的角度来看，最好从最容易执行的开始，前提是价值能够实现。这将让你摘下容易摘到的果实，并对你的方法建立信心，一旦你展示了回报的能力，你就可以要求更多的资源和资金。这一点尤其重要，因为这一层中的大多数问题都需要商业案例、资金和其他治理措施才能成功执行。

当您运行问题审核时，全面确定可能属于这一层的问题(即，我们是否能够使用数据来预测…？)并开始对它们进行优先排序。与之前的任何层级相比，您可能需要教育您的利益相关者什么是可能的，以及您应该做什么，因为某些计划可能:

1.  释放其他能力——基于客户终身价值模型的开发做出更明智的决策
2.  提供可以扩展或重新分配的技术，只需一点点努力，就可以解决具有一些相似特性的不同问题
3.  需要技术投资

也要认识到，这将主要是项目工作，所以他们将被交付的性质将发生变化，需要一个不同的管理风格相比，你的 BAU 工作。

最后，管理期望，让你的团队花大约 20%的时间在这些项目上，根据你的资源，你每年至少交付 2-3 个这样的项目()。也可以将这些项目留到最后，完全隐藏起来，直到您的所有第 1 层分析都得到解决，并且您已经取得了良好的进展，并为您的第 2 层和第 3 层开发了节奏。但是，您需要知道这些机会在哪里，一旦有机会，您需要找到时间(和正确的策略)来执行它们。

# 最后的想法

您可能会注意到，第 1 层和第 4 层都有一个自动化组件。在第 1 层中，您自动化简单性，而在第 4 层中，您自动化复杂性。其余的问题将是具体的，由上下文驱动的，因此很难自动化。有时，他们还需要对您的第 1 级和第 4 级回应产生的结果进行解释。

因此，他们也将成为你最可靠和最有价值的工作来源。在某些方面，您将把第 1 层的解释和决策部分委托给自助终端用户，将第 4 层委托给算法(这取决于技术，可能是黑盒本身)。然而，你将是第二层和第三层空间中任何事情的关键解释者和决策者，所以对这些问题承担责任和所有权，并确保它们占去了你投资管理工作的大部分时间。

祝好运和快乐(问题)审计！

**本文原载于**[**【https://datandi.com/】**](https://datandi.com/)