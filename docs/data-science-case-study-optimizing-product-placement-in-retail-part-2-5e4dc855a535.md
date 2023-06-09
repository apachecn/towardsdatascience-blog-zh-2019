# 数据科学案例研究:优化零售中的产品布局(第二部分)

> 原文：<https://towardsdatascience.com/data-science-case-study-optimizing-product-placement-in-retail-part-2-5e4dc855a535?source=collection_archive---------25----------------------->

## 商业模拟导论。

![](img/8d71d8eba5ce492c73ca32a3b25a23f6.png)

欢迎来到 2019 读者，感谢你抽出时间阅读这篇文章。距离我的上一篇帖子已经有一段时间了，但我肯定会完成我开始的工作。在我的上一篇文章中，我们使用销售数据来说明如何使用 XGBoost 的功能重要性来优化产品放置，这有助于确定哪个因素是最有影响力的，以及从那里应该选择哪个商店来销售特定的商品。在这篇文章中，我想回答一个不同的问题。

# 更进一步

如果我们想为我们的顾客开一家新的商店呢？假设我们与所有其他分店处于同一地理区域，我们如何决定**分店 _ 规模**、**分店 _ 位置 _ 类型**和**分店 _ 类型**？如果我们想加强我们在一个市场中的地位，我们可以采取这样的行动，此外，根据我们对客户的长期了解来设计我们的下一个销售点。

## 使用 Numpy 的 Argmax 函数

我想到的第一种方法是基于数据集“易处理”特征的可能值创建一个预测网格，然后使用 numpy 的 [argmax](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.argmax.html) 函数来确定哪个值将产生最大的奖励或支出。简单描述 argmax，可以描述为最大化某个函数 *f* 的集合 *x* 的值。这种方法受到了[决策分析](http://www.businessdictionary.com/definition/decision-theory.html)中一个叫做 [Maximax 准则](http://www.businessdictionary.com/definition/maximax-criterion.html)的概念的影响，在该准则中，所选择的策略是具有最高回报或支出的策略。下图说明了 argmax 函数的工作方式。

![](img/5e51147911cff30e0f455429d6c0ea76.png)

基于上图，值**“0”**最大化两个函数中的任何一个。所以 argmax 是 0。这种方法的问题在于，它假设只有一种行动或决策可以用来提高所选产品的销售预测。更好的方法是发现哪种组合或行动可以产生最佳预测，并确定的当前位置是否已经是最佳的。为此，我将研究蒙特卡罗树搜索算法。

# 使用蒙特卡罗树搜索

[Multi-Armed Bandit](https://en.wikipedia.org/wiki/Multi-armed_bandit) 问题是一个优化问题，其中一个代理寻求在一个状态空间内找到最大化系统支出的最优策略。我认为这种方法非常适合这种情况，因为可以采取许多行动(以及行动的组合)来找到最佳的产品放置。蒙特卡罗树搜索是一种发现最优策略(事件序列)并因此解决多臂绑定问题的方法。下图说明了蒙特卡洛树搜索的主要步骤:

![](img/48dad901c6b200d9771d5ef2b4945b2f.png)

Monte Carlo Tree Search

使用蒙特卡罗树搜索，可以找到产生最佳结果的动作组合(状态配置)。然而，应当注意，在这种特定情况下，所呈现的动作的组合并不意味着以任何特定的顺序来执行，而是同时执行。如果这听起来很熟悉，你可能记得这种技术也被用于 [AlphaGo](https://deepmind.com/blog/alphago-zero-learning-scratch/) 。如果你想对蒙特卡罗树搜索有一个全面深入的解释，[杰夫·布拉德伯里](https://twitter.com/jeff_bradberry/)在他的网站上有一篇精彩的[文章](https://jeffbradberry.com/author/jeff-bradberry/)解释了它的内部运作。

# 结论

值得注意的是，这种算法通常出现在“ ***完美系统*** ”用例中，例如游戏和模拟，其中系统的所有规则都是已知的，并且没有未知变量。不幸的是，生活不是这样的。应用于“假设”场景的机器学习技术仅用于提供关于什么可能产生最佳结果的指导。

尽管我们获得了销售数据，但我们仍然不确定观察到的购物习惯的季节性，这肯定会对推荐的质量产生影响。这个系统的一个更好的版本将能够找到多种产品的最佳放置选项，同时允许用户优先考虑一种产品。

我希望这篇文章给了你一个清晰而实用的方法，用你的数据科学为项目创造价值，我希望你能学到一些新的东西。这只是说明强化学习如何被用来为企业创造价值的一个实例。像往常一样，我欢迎您的反馈，并期待产生更多的内容。

要了解关于本文主题的更多信息，请访问下面的链接:

 [## 最大、马希民和极小后悔

### 马希民、极大极大和极小极大后悔是不确定条件下决策的三种方法。收益表显示…

kfknowledgebank.kaplan.co](http://kfknowledgebank.kaplan.co.uk/KFKB/Wiki%20Pages/Maximax,%20maximin%20and%20minimax%20regret.aspx) [](https://deepmind.com/research/alphago/) [## AlphaGo |深度思维

### 专家们将这篇论文描述为“在复杂领域走向纯粹强化学习的重要一步”。我们做了…

deepmind.com](https://deepmind.com/research/alphago/) [](https://jeffbradberry.com/posts/2015/09/intro-to-monte-carlo-tree-search/) [## 蒙特卡洛树搜索简介—杰夫·布拉德伯里

### 游戏 AI 的课题一般是从所谓的完美信息游戏开始的。这些是回合制游戏，其中…

jeffbradberry.com](https://jeffbradberry.com/posts/2015/09/intro-to-monte-carlo-tree-search/)