# 使用 Google BERT 训练弱标签、多标签数据:对来自 Westeros 和 Essos 的文档进行分类

> 原文：<https://towardsdatascience.com/training-weakly-labelled-multilabel-data-with-google-bert-classifying-documents-from-westeros-a2dda03e506e?source=collection_archive---------9----------------------->

## *背景知识:Google BERT，NLP 的一些知识*

**简介**

关于自然语言处理背景下的文本分类的论文大多处理整齐标记的数据，这些数据仅适合于一类(单标记多**类**分类问题；例如，图像包含或不包含猫)。

然而在现实世界中，我们经常不得不处理带有弱标签的数据，这不仅是因为 1)缺少标记数据的人力，而且 2)我们的问题通常是多标签的——一个文档有多个标签。(例如，图像可以有猫和狗)

此外，不同公司的分析师通常有非常具体的内部相关类别，这些类别无法整齐地归入商业 NLP APIs，如 Google Cloud ML。

我是 NLP 项目团队的一员，为一家金融机构做多标签文本分类。

我们在 NDA 之下，所以我不能透露我们在为哪家公司工作，或者具体的任务，所以我使用乔治·R·R·马丁的系列丛书中的名字来匿名化我的数据，并希望给你一个有趣的学习例子。

我将根据“火与冰之歌”虚构的宇宙给出一个问题描述，然后继续讨论我如何使用 Google BERT 来解决这个问题。

**问题描述**

想象以下场景:

*你是一名来自亚夏地的巫师，手持一面被称为“电脑”的神奇黑镜。国王之手* [*韦赛里斯二世坦格利安*](https://awoiaf.westeros.org/index.php/Viserys_II_Targaryen) *已经联系你帮助他。每天，他和他的工作人员都会收到涵盖维斯特洛和埃索斯所有政治实体的文件；大部分文件来自官方法庭，格式相似，但也包括其他来源，如信件和间谍报告。*

最终，国王之手想要做的是做出决定来维护王国的和平与繁荣，但是他和他的工作人员需要花费大量的时间来通读所有这些文件并将它们汇编成报告。

手和他的工作人员已经为你分类并验证了文件的样本，而用你的电脑，你可以神奇地获得一个文件样本，尽管没有来自烈酒的标签，名字像“Guugle”、“B'eeng”和“阿雅 Huu”。你还可以接触到一个名叫伯特的傀儡，他已经接受了超过六百万种交流方式的训练。

国王之手给你一定的时间来制作原型模型。随后，他会将您在“实时”数据上的结果与他自己的员工在相同数据上的表现进行比较。

基本上我们有:

1.  文档包含的不同标签的列表。(大房子，自由城市，其他派别)文件可以涵盖一个以上的类别。
2.  一个由人类验证的小样本(国王的手和他的杖)
3.  访问没有标签的附加文档(抓取在线数据)

我们将在“实时”数据上对国王之手及其幕僚进行测试。

**机器学习方法**

希望上面给了你一个有趣的比喻，来说明我们的问题，不要太混乱。

我是这样处理这个问题的:

按照吴恩达的指导方针，我们应该拥有训练、验证和测试数据集。

在最好的情况下，数据集应该彼此相似，但如果这不可能，我们至少应该让验证集与测试集相似。然后，我们在训练集上训练和调整超参数，以便在最终将其应用于测试集之前，在验证集上进行评估时获得良好的结果。

在这种情况下，我从 web 上搜集了大量文档，使用标题中的关键字作为弱标签。

例如，当我为史塔克家族搜集文件时，我会在 bing 上搜索“domain:" varys . com " intitle:" Brandon Stark " '，并将其视为“史塔克家族”的弱标签。

然后，我从收集的所有 HTML 和 PDF 文件中提取字符串，并将其全部放入一个大的数据帧中。之后，我在抓取的文本上对 BERT 进行了微调，以使 BERT 模型在“政治”语言上得到微调。

***第一次接近*** *:*

在这一点上，我最初的方法只是将整个文档作为一个整体输入并标记到 BERT 中，让它截断最终超过 512 个单词块标记的文档，并用我的单个弱标签标记该文档。

请记住，由于我刮的方式，每个文档只有一个弱标签，例如“史塔克家族”，但文档本身也可能提到“兰尼斯特家族”等等。

基本上，与“阴性”样本相比，我的每个标签只有很少的阳性样本，而事实上，很多“阴性”样本都是假阴性。在 1 万份文件中，从我搜集的数据来看，可能有 100 份被贴上了“豪斯·斯塔克”的标签，但实际上，剩下的 9900 份文件中，有很多可能也包含了有关“豪斯·斯塔克”的信息。

为了解决这个问题，在我的损失函数中( [sigmoid 与二元交叉熵损失](https://pytorch.org/docs/stable/nn.html#torch.nn.BCEWithLogitsLoss))我增加了阳性样本的权重。(pos_weight in PyTorch)凭直觉，我用* pos_weight 重要性来对待每个阳性样本。如果 pos_weight 为 10，那么我认为阳性样本的价值是“阴性”样本的 10 倍。

我优化的指标是 F1 综合得分，稍微偏向于回忆。

通过这种方法，我在验证集上获得了大约 0.35 的 F1 分数——F1 分数在训练 BERT 分类器的大约 5-6 个时期后趋于平稳。

这不是很好，比我的合作伙伴使用的使用 tf-idf 的经典机器学习算法还要差。

***第二种方法*** :

在这一点上，我认为截断的文本和缺少标签是使用 BERT 的一个巨大限制。

我创建了一个空间规则匹配器脚本，为每个标签匹配关键字。比如史塔克家，我会包括“史塔克、临冬城、布兰·史塔克、罗柏·史塔克”等等。只要匹配器选择了其中一个关键词，我就会用“1”标记该文章的类别(例如“House Stark”)。

然后，我根据原始字符串“\n”将文本分割成单独的段落，并对分割的文本运行规则匹配器脚本。

最后，我为这个特定的分类任务微调了我的 BERT 模型。

本质上，我是在用关键词训练 BERT 模型，并希望它能获得比关键词本身更多的上下文信息。

使用这种方法，我的 F1 分数在验证集上达到了大约 0.50，这比纯粹的“仅规则匹配器”模型要高。所以模型确实获得了额外的信息！

肯定还有改进的空间——在这一点上，我只将我朋友的性能与基于 tf-idf 的方法相匹配，坦率地说，仅仅为了获得与更老、计算成本更低的模型相匹配的值而训练 BERT 是浪费时间。

在这一点上，我认为要获得规则匹配器无法捕获的额外人类特征，我只需在验证集本身上微调模型，因为这是由人类专家手工标记的。

我这样做了，当它最终进入概念验证测试时，BERT matcher 本身确实产生了超过 tf-idf 模型的 F1 分数(大约 0.68)。

然而，最终我们实际上发现 BERT 模型和 tf-idf 模型的集合产生了甚至更好的 F1 分数。

**学习要点和改进途径**

查看博客和讨论板，并与我的一些同行交谈，我发现人们正在以不同的方式使用 BERT。[本文](https://arxiv.org/abs/1903.05987)描述了两个主要部分:1)将“冻结”的权重作为一个特性用于下游任务，2)解冻权重并针对特定任务对其进行微调。在论文中，它们被表示为冰(❄️) ️and 火(🔥)分别。

我选择了火🔥我认为那篇论文证明了伯特用这种方法确实比用冰❄️方法表现得更好。我怀疑这可能是由于伯特在❄️方法中失去了理解上下文的能力。

在上面的任务中，当在验证集上微调模型时，我也简单地使用了默认的 BERT 方法输入文本——也就是说，它涉及到截断超过最大序列长度的文本。

最近的一篇中文论文提到，结合文档的开头和结尾有助于提高他们对长文档的分数。我计划在模型的未来迭代中实现这一点。

我也一直在研究[通气管](https://github.com/HazyResearch/snorkel)，它可以帮助你为弱标签创建一个概率模型，只要你有一些“黄金标准”，人类验证的数据与之比较。

**结论**

在现实世界中，带标签的数据是一种奢侈品，你必须想办法在机器学习任务中使用弱标签。在特定领域语言上训练 BERT 模型，然后在基于关键字的“弱标签”上对其进行微调，最后在人类验证的数据集上对其进行微调，似乎可以产生超过传统 NLP 模型的结果。