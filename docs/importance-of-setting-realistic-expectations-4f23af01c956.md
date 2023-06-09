# 设定现实期望的重要性

> 原文：<https://towardsdatascience.com/importance-of-setting-realistic-expectations-4f23af01c956?source=collection_archive---------37----------------------->

![](img/f59e85406e7b8e199e606cabe0308800.png)

## 如果产品所有者有现实的期望，你的模型会更快地产生更大的影响

似乎每个公司现在都在建立数据科学团队，并投资机器学习平台，无论是第三方还是内部构建的。

然而，研究表明，很少有公司将机器学习模型部署到生产中[1]。虽然技术复杂性是原因之一，但不切实际的期望也是原因之一。

# 设定合理的期望值

开发机器学习模型需要大量投资。你需要雇佣数据科学家，投资大数据工具，建立/购买模型服务平台。因此，期望往往很高，有时过高。

为了确保人工智能项目的成功，数据科学家需要确保他们在开始建立模型之前就设定了现实的预期。如果预期无法实现，您将获得开发模型的批准，但它们永远不会投入生产。

设定期望可能会很复杂，但你可以做一些事情来帮助引导对话:

*   使用现有流程作为基线
*   谈谈误报和漏报——你在优化什么？
*   用一个简单的模型来设定期望值

# 使用现有流程作为基线

机器学习模型通常会取代或自动化现有流程。查看这些流程，并尝试量化其整体性能(准确性、假阳性/假阴性率、预测时间等)。这将给你一个你的模型需要达到的基线。

> *除非您的模型与现有流程的性能相匹配，否则无论节省多少成本，都不会部署该模型*

不要花太多时间考虑解决方案的总体成本，更多地关注整体模型的性能。这里的目标不是定义企业通过实施机器学习解决方案可以节省多少成本，而是了解您的模型预计将达到什么样的性能水平。

# 定义可接受的误报率和漏报率

在设定期望值时，我们首先考虑的是准确性。它很容易理解，通常是与产品负责人交谈时的神起点。

然而，仅仅同意一个目标精度是不够的。几乎在所有应用中，误报的业务成本都不同于漏报的成本。在很多情况下，成本可以相差一个数量级！

以欺诈预测为例。让我们假设你以 100 英镑的价格出售一件产品，利润率为 20%。这意味着一次销售将产生 20 英镑的利润但如果有人用偷来的卡购买产品你将损失 80 英镑(生产成本)外加支付处理商收取的费用(可能在 20 英镑左右)。在这种情况下，误报的成本是 20，而误报的成本是 100！因此，你的模型理论上可以有一个比假阳性率高 5 倍的假阴性率，并且仍然是有利可图的。

# 用一个简单的模型来设定期望值

部署一个机器学习模型涉及许多活动部件，从服务到监控。您部署的第一个模型必须相对简单，因为重点是围绕该模型的基础设施和流程。

> *模型的第一次迭代是关于建立流程，而不是关于性能*

在花太多时间在其他事情上之前，开始开发一个非常简单的模型，很少或没有特征工程。假设这将是部署的第一个模型。

如果简单模型没有达到在阶段 1 和阶段 2 中与产品所有者达成一致的指标，您可以采取两种方法:

*   构建特征处理和复杂的模型，但是由于部署成本的原因，存在无法部署模型的风险
*   让产品负责人重新参与进来，为模型的第一个版本设定更现实的期望

在这些选项之间进行选择将取决于您的组织以及您正在开发的模型的战略性。在任何情况下，不要在没有与产品负责人讨论之前就开始。这可能看起来不多，但这可以将开发周期加快 10 倍。

# 结论

为了让机器学习模型在组织中得到广泛采用，数据科学团队需要在构建第一个模型之前让业务参与进来。

在项目开始时就性能度量标准达成一致，并定期与产品所有者进行核对，将有助于确保模型被快速部署。

参考资料:

*   [1]: [BCG-MIT 报告:2018 年人工智能在商业中的进展](https://www.linkedin.com/pulse/bcg-mit-report-progress-ai-business-2018-philipp-a-gerbert)