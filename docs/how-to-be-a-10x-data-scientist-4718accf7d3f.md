# 如何成为 10 倍数据科学家

> 原文：<https://towardsdatascience.com/how-to-be-a-10x-data-scientist-4718accf7d3f?source=collection_archive---------9----------------------->

![](img/af49767a4f9de73504cde215dc46963c.png)

我将告诉你成为 10 倍数据科学家需要什么。什么是 10x 数据科学家？一个比普通数据科学家多做十倍实验的人。

为什么要做实验？数据科学家也做其他事情:数据管理、分析和为生产编写机器学习算法的实现。但是实验是数据科学家的定义。这就是科学的所在，也是他们区别于数据分析师或机器学习工程师的地方。

因此，要成为一名伟大的数据科学家，你必须擅长做实验。

为什么要多做 10 倍的实验？你永远不能保证你会因为更聪明或更快而获得十倍的好结果。但是你可以做更多的实验。你做的实验越多，你得到更好结果的可能性就越大，你迭代的速度就越快，你学习的速度也就越快。

你为什么想成为 10x 数据科学家？我不知道。可能因为听起来很酷。可能因为好玩吧。也许因为你会有更多的时间吃糕点。这取决于你。

我假设你能正确地进行实验。你是数据科学家，对吧？然而，有一件事我见过许多数据科学家犯了错误。是这样的:

# 1.衡量你的不确定性

如果不知道结果是否具有统计学意义，那么在基线上提高 5%有什么意义呢？数据科学家知道(或者说*应该*知道)统计学，但是他们往往懒得把它应用到自己的工作中。

这方面并不缺乏选择。我最喜欢的方法是我在物理学学位中学到的:将不确定性估计为平均值的[标准误差](https://en.wikipedia.org/wiki/Standard_error)。当然，这意味着您报告的值必须是某个值的平均值，无论是交叉验证中五次折叠的平均 F1 分数，还是 1000 个不同查询的排名中 10 的平均精度。

你不需要在所有结果之间做统计显著性检验。但是你需要知道你的结果有多不确定。平均值的标准误差给出了这一结果——如果您的结果相差超过标准误差的三倍，则差异可能非常显著。

你可能还想考虑一下你想要什么样的效果尺寸。如果 0.1%的改进对你没有用，那么进行可以检测这种变化的实验就没有意义了。

# 2.大数据并不酷

大数据慢。你不想慢下来。所以用小数据。大多数时候你不*需要*大数据。如果你认为你需要它，花一点时间重新考虑，以确保你真的需要它。

您希望您的数据集足够大，以便您的结果中的不确定性足够小，足以区分您所关心的差异。你不想让它变得更大:那只是浪费时间。

你不必使用所有可用的数据。根据您的实验，您可能能够估计您需要多少数据。否则，看看您所关心的指标是如何随着训练集的大小而变化的。如果它相当快地稳定下来，你就会知道你可以丢弃很多数据。做更多的实验，弄清楚你需要多少数据来使不确定性足够低，以获得你正在寻找的洞察力。

实验缓慢的首要原因是使用了太多的数据。就是不做。

# 3.不要使用大数据工具

如果你有小数据，就不需要大数据工具。不要使用 Spark，它会慢得可怕，与熊猫和 Scikit-learn 相比，结果会很差。用那个代替。

# 4.使用好的 IDE

使用一个像样的集成开发环境，比如[PyCharm](https://www.jetbrains.com/pycharm/)——实际上，只是使用 py charm，没有什么真正的比较。学习如何正确使用它。

这些是我觉得最有用的东西:

*   自动完成，尤其是与键入的代码结合使用时
*   查看函数或类的参数和文档
*   快速搜索文件、类或函数的整个代码库
*   重构以提取变量、函数或方法以及内联变量

我不忍心看着人们为了这种事情和一个文本编辑器较劲。请停下来。

Jupyter 笔记本做探索性工作还可以，但是如果你想成为 10x 的数据科学家，你需要用一个 IDE 做实验。

# 5.缓存中间步骤

实验可以包括数据预处理、特征提取、特征选择等。这些步骤中的每一步都需要时间来运行。一旦你找到了一组好的特性，你就可以在实验模型的时候或多或少地保持它们不变。如果预处理步骤需要很长时间，缓存中间步骤是有意义的，这样您只需执行一次这些昂贵的计算。这将对实验进行的时间产生巨大的影响。

我通常会使用一个或多个预处理脚本来完成这项工作，这些脚本会生成供后续阶段使用的文件。确保您跟踪这些文件如何与源数据相关，以便您可以通过文件命名约定或为工作设计的工具(如 [Pachyderm](https://www.pachyderm.io/) )将您的实验结果追溯到原始数据。

# 6.优化您的代码

如果您的实验在减少数据集大小后仍然很慢，那么您可能会从优化代码中受益。在运行实验的同时，平衡运行实验和优化代码。

你应该知道如何优化代码的基本知识。这里是基本的:使用一个分析器。分析器会告诉你哪些位是慢的。改变这些位，直到它们不再慢为止。然后运行分析器，找到其他慢的位。重复一遍。

在一个小样本上运行分析器，这样您就可以快速找出哪些位运行缓慢。(你也需要优化优化。)

# 7.记录你的结果

如果你丢失了实验结果，那就是浪费。所以要小心追踪。使用为工作设计的工具，比如 [MLFlow](https://mlflow.org/) 、[圣物](https://github.com/IDSIA/sacred)，或者我自己的宠物项目 [PyPastry](https://github.com/datapastry/pypastry) 。如果你到处复制结果，你是在浪费时间，而且很可能出错。不要。

如果你做了以上所有的事情，运行一个实验可能需要不到五分钟，理想情况下不到两分钟。这段时间足够思考下一个实验会是什么。

这意味着你有可能在一天内运行数百个实验。当你运行这么多实验时，你需要一个好的方法来跟踪。

# 7a。多吃糕点

这实际上不是一个好建议。你的大脑每天需要高达 400 卡路里的葡萄糖，但吃糕点可能不是实现这一目标的最健康的选择。但是会很好吃。

相反，你可以考虑联系 [DataPastry](https://datapastry.com) ，这是一家数据科学咨询公司，我和我的联合创始人 Iskander 一起经营。如果您想要任何建议或需要数据科学项目方面的帮助，[我们很乐意收到您的来信](mailto:hello@datapastry.com)，我们不咬人(糕点除外)。

# 结论

如果你做了以上所有的事情，我很确定你会比坐在你旁边的数据科学家至少多做十倍的实验(除非你坐在我旁边)。大部分数据科学家都不做。所以如果你都做了，你可能会多做五十次实验。这让你变得更有价值 50 倍吗？我不知道，但这没什么坏处。你会有更多的时间吃糕点。

*原载于 2019 年 10 月 1 日*[*https://datapastry.com*](https://datapastry.com/blog/how-to-be-a-10x-data-scientist/)*。*