# 精益预测工作流程

> 原文：<https://towardsdatascience.com/a-lean-forecasting-workflow-1a8a5eb2d4ab?source=collection_archive---------23----------------------->

## 如何使用精益数据科学工作流程创建良好的业务预测

![](img/a4bb4583033be9960069a46b7dbc3d13.png)

Photo by [Felix Wegerer](https://unsplash.com/@felixwegerer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

商业预测的工作基本上类似于典型的数据科学项目，但是它需要自己的调整才能正确完成。在本文中，我们打算应用精益框架，不仅产生良好的预测，而且确保您的流程为预测质量增值。

在这里，我们预测问题的例子将是预测一个零售连锁店的收入，但是它可以应用于许多其他用例。

## 工作流程

## 请求

这是你的客户提出他的预测请求的地方，你将开始发展你的业务理解。你可能有的许多问题会在这个过程的后期出现，但是没关系:只要确保你在一开始就已经涵盖了最重要的主题。以下是一些有用的问题:

*   这些预测的目标是什么(了解你的总收入结构，指导生产决策，向股东报告…)？
*   它们将如何被使用(它们应该被发送到一个漂亮的仪表板还是将被发送到另一个自动化系统)？
*   谁会使用它们(是精通数据科学的人，公司的 CEO，投资者…)？
*   我们会维护它们吗？谁来做？—我们稍后将详细讨论如何维护预测
*   你想什么时候完成(截止日期是什么时候)？
*   在什么水平上(整体、按商店、按产品……)？
*   在什么时间段(每周，每月…)？
*   我们将提前多长时间生成预测(下周、明年……)？
*   是否有要使用的外部数据(天气、假期……)？

## 技术设置

在这里，您可以选择生成预测的工具或编程语言，还可以设计文件夹结构(如果适用)。就我个人而言，我喜欢每个步骤都有一个 Jupyter 笔记本:数据处理、分析和建模，但可以自由选择最适合你的。

这应考虑是否将预测发送到仪表板或存储您的数据的自动化系统，如果您的客户已经有一个预测系统，您打算如何获取外部数据，以及预测是否将被维护(以及由谁维护)。

在这一点上，你还必须设计你的数据工作流程:列出你的数据源，它们是如何被收集、存储和合并的，以及你的脚本在哪里。笔和纸在这里可能会有帮助。

## 数据处理

首先创建数据提取脚本:这些可能是来自数据库的查询，但也可能包括某种 web 清理。考虑所需的聚合级别、外部变量和时间框架。

一旦收集了数据，您将不得不清理它，这将提出一些常见的问题，例如如何处理离群值和缺失值？嗯，这个真的要看每个具体案例，我也不能真的给你提供一个最终的答案，但是试着问问自己:为什么这个值这么高/缺失？是真值，还是很可能是输入错误？然后考虑如何处理它:用一些公式(比如平均值)手动输入它，去掉它，用零代替它，等等。

最后，你会做一些特征工程:合并不同来源的数据，添加新的变量，现有变量的组合或函数(log，平方根等。)等等。你不必在这里面面俱到，如果需要的话，你可以稍后回到这一步，添加你在开始时没有想到的变量。

## 分析

这是你让你的好奇心自由奔跑的地方，并且真正理解你正在处理什么类型的数据。然而，这里可以回答几个问题作为进一步分析的起点:有趋势吗？这个时间序列是平稳的吗？有季节性吗？在什么级别(每天、每周…)？如果有外部变量，它们是如何相互作用的(尤其是与你试图预测的变量)？您可以为多对变量创建多个散点图。如果您发现您感兴趣的变量和另一个变量之间的关系具有某种特殊的形状，您可以返回到上一步，尝试在该变量上包含变换。例如，您可能会看到您的收入与观察到的降雨量有关，但不是以线性方式。

在分析过程中，您还需要根据数据定义适当的误差测量。常见的误差度量包括 RMSE、MAPE 和脉塞，但还有更多。根据你的目标和数据做出明智的选择。:MAPE 不适用于间歇性数据，即变量经常等于零的情况)。

一旦您定义了您的误差度量，您需要设置正确的基线:从现在开始，您将根据它来比较您获得的误差与您尝试的所有模型。你的基线是你用最简单的模型得到的误差。例如，如果您正在处理零售收入，该收入具有很强的年度季节性，您可以将明年 12 月的销售额预测为去年 12 月的销售额。你不需要一个奇特的模型或数据科学家来做这件事:一个 Excel 电子表格就可以了。因此，这是可接受的最大误差值，如果你的神经网络不能战胜它，那么它肯定不值得努力。低于这个级别的任何东西都可以被认为是一种改进，但是请记住，您可能不想为了几个额外的准确性点而牺牲可伸缩性和易于理解性。

现在你有了基线，你可以考虑适合你情况的模型。一些模型不处理季节性，而另一些不处理外部变量。现在有太多的方法，你不可能知道所有的方法，但是一定要列出所有的基本方法(这些方法往往执行得很好)和一些更高级的方法。基础知识包括 SARIMAX 系列模型和指数平滑方法。更复杂的方法包括使用 XGBoost、神经网络或脸书开发的 Prophet 算法。

## 系统模型化

建模部分本身是非常简单的，它将为返回到您的数据处理和分析步骤以及添加额外的变量和分析提供洞察力。

首先，您将把数据集分成三部分:训练、验证和测试。验证/测试术语通常有些混乱，但在这里，我假设训练数据用于训练您的模型，验证用于应用它们，查看哪个效果最好，并可能使用 insight 来更改一些超参数，测试集是您应用您的最佳模型并获得关于它在新数据上的表现的良好估计的地方。与其他数据科学问题不同，这种分裂不应该是随机的:因为你正在处理时间序列，所以你的观察顺序很重要，你应该保持这种顺序。相反，为每个数据集选择一个分割点(一个日期)。《出埃及记》:我将从 2015 年到 2018 年训练我的模型数据，在 2019 年的数据上验证它们，并在 2020 年的数据上测试我的最终模型。

但是，请记住，如果您的模型依赖于在它必须预测之前发生的观察，这种方法是不完整的。例如，如果您的模型应该根据过去三周来预测下周的预测，您将需要执行向前行走验证，这意味着当您每周进行预测时，您的训练集会逐渐变大。你可以在这里阅读更多相关信息[。](https://medium.com/eatpredlove/time-series-cross-validation-a-walk-forward-approach-in-python-8534dd1db51a)

## 重复

通过应用所有这些模型，您肯定会了解更多关于您的数据行为的信息，这意味着您将通过数据处理和分析，甚至通过请求阶段，向您的客户询问您以前没有想到的问题并添加新功能。你这样做，直到你根据你的基线取得了令人满意的结果，或者如果你已经达到了客户给你的最后期限(或者如果你已经没有改进的想法了，很明显)。

## 同意

在许多情况下，您需要客户或更高层的批准来部署您的模型，这意味着您必须向他们展示您已经尝试过的模型、获得的结果，以及与基线相比您实现了多少。根据这些人是谁，您可能希望保持简单，或者更详细地了解度量和方法。但是，请确保您向他们现实地展示了他们可以从您的预测中得到什么(此处应使用预测置信区间)。

## 部署

到了部署的时候，您将使用您选择的基础设施来部署您的数据处理步骤，以及一个模型应用步骤，只包括您决定应用的模型(您不需要在这里继续测试模型，也不需要分析部分)。

## 监视

为了监控您的模型，您需要记住您想要跟踪的度量标准。不应该有太多(通常三个就足够了)，他们至少应该测量偏差，平均误差和方差。除了这些指标之外，您还需要跟踪您的预测置信区间和实际观察值:确定一个可接受的误差阈值，无论何时您的预测开始偏离轨道，您的监控系统都应该发出某种标志。

# 结论

我希望这篇文章对您和您的预测需求有用，并记住这是整个工作流的一般指南，但这些步骤中的每一个可能都值得有自己的文章，因为每个步骤都有许多警告和注意点(我可能很快就会在这方面工作)。

# 有用的链接

[本文展示了一个数据科学工作流的示例，并附有实际例子。](/the-data-science-workflow-43859db0415)

[这家公司也有类似的目标，但重点是初创公司。](/data-science-project-flow-for-startups-282a93d4508d)

[数据科学项目的模板(一种可以复制的文件夹结构)。](https://drivendata.github.io/cookiecutter-data-science/)

网飞管理数据科学项目的图书馆 meta flow。

[脸书的先知，一个时间序列预测的优秀图书馆](https://facebook.github.io/prophet/docs/quick_start.html)。