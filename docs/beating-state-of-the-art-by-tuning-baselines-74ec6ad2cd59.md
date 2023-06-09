# 通过调整基线超越最先进水平

> 原文：<https://towardsdatascience.com/beating-state-of-the-art-by-tuning-baselines-74ec6ad2cd59?source=collection_archive---------11----------------------->

你如何知道一个新的机器学习模型是否是对以前模型的改进？一种方法是将其与为相同任务开发的基线模型进行比较。但这回避了一个问题:你如何知道基线本身是否好？由 Rendle，Zhang & Koren 撰写的一份新的预印本“[关于评估基线的难度:关于推荐系统的研究](https://arxiv.org/abs/1905.01395?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog)”表明，衡量一个基线模型对一个具体问题的效果并不像它初看起来那样简单。事实上，**的作者仅仅通过调整基线并将它们与简单的、众所周知的方法结合起来**，就能够在 [Movielens 10M 基准](https://grouplens.org/datasets/movielens/10m/?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog) **上击败当前最先进的**的推荐。

![](img/9d79d170d792184105964e59a7cd6878.png)

Blue x’s are the results reported by authors for their newly-proposed method, black/grey triangles are the baselines those authors run… and red are the tuned baselines. Down is better and, as you can see, after additional turning ([as outlined in the paper](https://arxiv.org/abs/1905.01395)) the tuned baselines are the most down (i.e. best performing).

# 我们如何评价机器学习模型？

我们先退一步。我们目前如何评估模型？

如果你曾经参加过 [Kaggle 竞赛](https://www.kaggle.com/competitions?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog)，你可能已经知道它们是如何工作的:你被给予训练数据来建立一个模型，为一个特定的指标进行优化。然后，根据不同的数据集对您的模型以及其他所有人的模型进行评估，并根据目标指标进行排名。提交结束后，每个人的模型都会在第三个看不见的数据集上排名，表现最好的模型胜出！(当然，前提是他们遵守了特定比赛的规则。)

然而，对于机器学习的学术研究来说，事情有点不同。一般来说，研究人员使用特定任务的数据为该任务建立新的模型。一些例子:

*   使用 [Netflix 奖项数据集的推荐系统](https://www.kaggle.com/netflix-inc/netflix-prize-data?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog)
*   使用[微软 COCO 数据集](http://cocodataset.org/?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog)进行对象分割
*   使用 [TIMIT 语料库](https://catalog.ldc.upenn.edu/LDC93S1?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog)进行语音识别
*   自然语言理解使用[胶水基准](https://gluebenchmark.com/?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog)

然后，他们将算法的性能与在同一数据集上运行的基线进行比较。如果这是一项已经存在一段时间的任务，通常会将你的系统与另一篇论文中报告的结果进行比较，但对于较新的任务，研究人员通常自己运行基线。

> 一个**基准**是一个包括数据集和评估性能的方法的任务。一个**基线**是一个众所周知的算法，可以应用于基准问题。

在研究中没有“获胜”的模式，但是提出一种新方法，然后证明它比以前建立的方法有所改进的论文往往会被发表。(对于研究人员来说，雇佣和晋升是基于发表论文的数量和质量，所以让你的论文发表是一件好事！)

这两个社区之间最大的不同可能是研究人员面临着关注新型模型的压力。如果一个老型号在 Kaggle 比赛中真的有效，竞争者没有理由不使用它…但是**如果主要发现是“我们已经做了十年的东西实际上仍然非常好”**，就很难让论文发表。

# 为什么基线一开始就不太好？

> 进行实验是困难的，需要大量的实验努力才能获得可靠的结果。(伦德尔等人，第 9 页)

重申一下:运行机器学习实验很难。Rendle 和合著者指出了调优可能出错的两个地方:

1) **在调整超参数**时，您很容易错过最佳时机。您的搜索空间的边界可能太靠近，或者在一个方向上移动得太远。您可能没有使用正确的搜索网格。你在小模型上得到的结果实际上可能不会放大。简而言之:很难很好地调优模型，而且很容易搞砸。

2) **在预处理或学习过程中，你可能会遗漏一些小而重要的步骤**。你打乱了你的训练数据吗？做 z 变换？你使用提前停车吗？所有这些选择都会影响你的模型结果。尤其是如果你试图复制别人的结果，这些步骤可能很难做对。(特别是如果它们没有被报告，并且原作者没有发布它们的代码！)

即使您做了所有您应该做的事情，并且有一个非常坚实的基线，基线算法可能会在额外的调整下表现得更好——特别是由非常熟悉该方法并且知道所有提示和技巧的人来调整。了解什么最适合特定的模式需要大量的试验和错误；这也是调整基线如此困难的部分原因。即使一篇论文的作者真的尽了最大努力来调整基线，有更多经验或稍微不同的方法的人可能会得到更好的结果。(有点像 Kaggle 比赛；与只使用过几次的人相比，非常熟悉 XGBoost 模型调优的人可能会得到更好的结果。)

而且，虽然在 Kaggle 式的竞争中有投入大量时间调优模型的动机，包括您的基线(如果它表现良好，您使用什么工具并不重要！)，**研究场所一般不会奖励花费大量时间调基线**。事实上，如果调整显示基线优于你想出的方法，这实际上可能会让*更难*发表一篇描述你的新模型的论文。这类似于[“文件抽屉问题”](https://www.psychfiledrawer.org/TheFiledrawerProblem.php?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog)，研究人员不太可能报告负面结果。

# 那么我们能做些什么呢？

Rendle 等人提出了两件事可以在这里有所帮助:标准化基准和激励机器学习社区投入时间调整这些基准。

## 不要多此一举

“重新发明轮子”意味着重新做已经做过的工作。**如果某个特定任务有一个已经很好调整过的既定基准，那么你应该与那个基准进行比较！**(额外的好处是，如果您正在进行一项既定的任务，并且可以使用报告的结果而不是重新运行它们，那么您可以节省时间和计算。🤑)

## 激励跑步(和调音！)基线

这个有点棘手:要改变一个已建立的社区的激励结构或价值体系极其困难。作者指出，机器学习竞赛，无论是在像 [Kaggle](https://www.kaggle.com/competitions?utm_medium=blog&utm_source=medium&utm_campaign=baselines-blog) 这样的平台上，还是在研究社区内组织，都是这样做的一种方式。我还要补充一点，如果你评论机器学习的论文，既要考虑新颖性(这种方法是新的吗？)和效用(这篇论文对整个社区有好处吗？)写评论的时候。

# TL；速度三角形定位法(dead reckoning)

仅仅因为最近提出了一种建模技术，并不意味着它一定会优于一种更老的方法(即使论文中的结果表明它可以)。调整模型需要时间和专业知识，但通过仔细调整，已建立的基线可以表现得非常好，甚至超过最先进的水平。依靠具有良好调整的基线的标准化基准可以帮助减少重复工作，还可以获得更可靠的结果。而且，如果您只是在为一个特定的项目寻找最佳方法，那么从更好理解的模型开始可能会更好。

如果你有兴趣阅读整篇文章，特别是关于不同推荐系统的基线调整的细节，你可以[在 Arxiv](https://arxiv.org/pdf/1905.01395.pdf) 上查看。