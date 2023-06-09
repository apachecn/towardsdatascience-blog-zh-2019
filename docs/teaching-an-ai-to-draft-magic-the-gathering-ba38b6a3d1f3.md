# 教人工智能起草魔法:聚会

> 原文：<https://towardsdatascience.com/teaching-an-ai-to-draft-magic-the-gathering-ba38b6a3d1f3?source=collection_archive---------6----------------------->

## 或者，如何训练你的机器人来训练你的龙

![](img/b89ab9bb2875b0a30293b8f13d1c40af.png)

# 概观

在《魔术:收集草稿》中，玩家反复地从一副牌中选择卡片，尽可能地制作出最好的一副牌。使用人类进行的草稿中的数据，我训练了一个神经网络来预测人类将从每副牌中取出什么牌。在这项任务中，它达到了 60%的准确率。在 40%的情况下，当人和模型不同时，模型的预测选择往往比人的选择更好。可以在[这里](https://github.com/zswitten/trophy-leader/blob/master/DraftbotKeras-Flooey.ipynb)找到一个笔记本，上面有模型训练代码和样本结果。

# 词汇表

*   魔术:聚会[MTG]:有史以来最好的纸牌游戏。“有点像扑克和象棋的结合，但是有龙”，这是我在去比赛的路上对拼车司机描述的。作为一名玩家，你召唤并指挥各种各样的神话生物，然后当你们两个施展魔法将它们推向更高的高度时，它们与对手的生物一决雌雄。
*   构造:MTG 最常见的玩法。比赛开始前，每个玩家制作一副 60 张的牌，并把它带到战场上。优点:自我表达(你可以选择你的牌组中放什么牌)。缺点:必须提前获得所有该死的卡($$$)。
*   草稿:在作者看来，扮演 MTG 最好玩的方式。你和其他 7 名玩家围坐在一张桌子旁。你们每人打开一包 15 张的卡片。你从你的包里抽出一张牌，然后把剩下的 14 张递给你的左边。你从这 14 张牌中抽出一张，然后把 13 张递给你的左边。重复，直到所有的牌都没了；现在你面前有 15 张牌。然后循环又开始了:你和其他 7 个人每人打开第二包。重复第三次，你有 45 张牌。然后用你起草的卡片做最好的一副牌。选秀的美妙之处在于，每个人都是在一个公平的竞争环境中开始的，而且每次都是不同的，因为你永远不会两次选择同一副牌。

要掌握草稿，你必须平衡每张牌的原始能量水平，牌与牌之间的协同作用，以及你在任何给定时间从剩余牌中接收到的信号。

# 培训用数据

[魔法工厂](https://magic.flooey.org)的老板好心地给我发了一个. json 文件，里面有第二部最新的 MTG 系列《拉夫尼卡行会》的 2130 份草稿。

我还搜集了 draft sim 的档案，在这个网站上，人们可以按照预先设定的挑选顺序练习与机器人对抗。根据这一数据训练的模型与根据 Flooey 数据训练的模型达到了类似的准确性水平，但我注意到模型做出了更差的选择，因为 Draftsim 用户比 Flooey 用户做出了更差的选择，可能是因为他们没有参与赌注。尽管 Draftsim 比 draft sim 多几个数量级。

# 数据表示法

为了表示一副牌中可供选择的牌的集合，我们可以使用一个长度为 N 的向量，其中 N 是 Ravnica (250)的公会中不同牌的数量。每张卡都有一个索引。您看到的第一副牌中有 15 张牌，因此它的向量将有 15 个 1(该副牌中牌的索引)和 235 个 0。第二个包将有 14 个 1 和 236 个 0，等等。

为了表示我们已经选择的卡片，我们可以使用另一个长度为 N 的向量，其中每个索引处的值是我们已经起草的卡片的编号。每次选秀的第一个选秀权都是零。对于第二次选择，将有 1 个 1 和 249 个 0。对于第三次选择，它可能是 2 个 1 和 248 个 0…除非我们从前两包中取出同一张牌，在这种情况下，它将是 2 和 249 个 0。

总之，我们模型的输入是一个长度为 2N 的向量。

输出是一个长度为 N 的独热编码向量，在人拿的牌的索引处被设置为 1，在其他地方被设置为 0。

这种表示忽略了草稿的一个重要特征:记忆你在之前的一副牌中看到的和没有拿到的牌。职业玩家使用这些信息来猜测他们在未来的牌包中可能会看到什么牌。我们可以通过给每个输入增加额外的 45 个长度为 N 的向量来表示。这些向量中的第一个将代表我们第一次选择时看到的牌，除非这个*是我们的第一次选择，在这种情况下，它都是零。一般来说，这些向量的第 K 个代表我们在第 K 次选择时看到的牌，如果我们确实已经进行了 K 次选择，否则都是零。

在模型中包含这些信息会将输入表示的大小乘以 24，这对于只有 2000x45 个数据点的情况来说并不理想。随着更多的数据，我认为这可能是一个有价值的功能添加。

# 建模

我试验了一个线性 SGD 分类器，它达到了 50%的准确率。然后，我尝试了一个神经网络，它有两个 512 个神经元的密集层，中间有一个 N 长度的 softmax 层，准确率达到了 59%。

# 定性评价

我浏览了测试集中的一些草稿，让模型在每个阶段说出它会选择哪张牌，给定已经选择的牌，以及人类选择的牌。你可以在这篇文章附带的笔记本中看到它们。

模特绝对理解色彩的概念。在 MTG 有 5 种颜色，任何给定的草稿牌都可能只使用其中 2 或 3 种颜色的牌。因此，如果你已经拿了一张蓝卡，你应该更有可能在未来的选择中拿蓝卡。我们没有告诉这个模型，我们也没有告诉它哪些牌是什么颜色。但不管怎样，它还是学会了，通过观察哪些卡片经常是相互组合的。

由于 MTG 问题还没有像国际象棋和围棋那样得到解决，所以不可能确切地说模型的选择有多好。我是一名[正派玩家](http://www.mtgeloproject.net/index.php?lastname=Witten&firstname=zack&search=Search)，当我看牌时，我看不出有什么明显的问题。事实上，当它和人类绘图员意见不一致时，我发现我倾向于更喜欢模型的选择。但我有偏见，所以请你自己看看这些精选，然后告诉我你的想法，或者让你最了解 MTG 的朋友去看看，然后反馈回来。

# 毫无根据的猜测

让一千个人猜一大罐软糖里有多少颗软糖。平均每个猜测的绝对误差。然后平均猜测值，取*that*的绝对误差。后者会少错一些。
http://wisdomofcrowds . blogspot . com/2009/12/chapter-one-part-I . html

我认为类似的事情正在这里发生。每个人都高估一些牌，低估另一些牌。将所有这些误差平均在一起，你会得到一个更好的结果。

# 未来的工作

如果我们对训练集中的每副牌都有匹配结果(即，每副牌最终赢了多少局)，我们可以让模型不仅针对与人类选择的相似性进行优化，还针对进行给定选择后预期牌的质量进行优化。对于一副牌中的每一张牌，模型会从这一点出发，设想出成千上万种可能的走法，并评估最终的牌组。然后它拿走给它最好的梦的卡片。也就是说，我们可以全力以赴[阿尔法零](https://en.wikipedia.org/wiki/AlphaZero)。

另一个令人兴奋的可能性是将来自 [MTGJSON](https://mtgjson.com/) 的数据添加到模型中。现在，每张卡只是 1 到 250 之间的随机整数。有了来自 MTG JSON 的信息，我们将添加关于哪些卡片是相似的明确信息。这将允许模型起草一个新的集合，而不用看到人类先起草它。

直到下一次，愿你无法区分足够先进的魔法和技术。