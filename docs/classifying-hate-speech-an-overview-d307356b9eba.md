# 仇恨言论的分类:概述

> 原文：<https://towardsdatascience.com/classifying-hate-speech-an-overview-d307356b9eba?source=collection_archive---------10----------------------->

## 浅谈标签分类和仇恨言论

由[雅各布·克拉布](https://medium.com/u/58811da7f0c1?source=post_page-----d307356b9eba--------------------------------)、[雪莉·杨](https://medium.com/u/e86e1bcb017?source=post_page-----d307356b9eba--------------------------------)和[安娜·祖波娃](https://medium.com/u/1c39b72311e2?source=post_page-----d307356b9eba--------------------------------)主演。

![](img/3cf16ca0856ecec7076db112b477aa80.png)

# 什么是仇恨言论？

争论仇恨言论是一个古老的挑战，但今天仇恨言论的规模、个性化和速度是一个独特的现代困境。虽然仇恨言论没有确切的定义，但一般来说，这种言论不仅仅是为了侮辱或嘲笑，而是通过攻击目标独特的东西来骚扰和造成持久的痛苦。仇恨言论在在线论坛、聊天室和社交媒体中尤为普遍。

[Hatebase.org](https://hatebase.org/)，一家加拿大公司，创建了一个多语种仇恨言论词汇词典，有以下识别仇恨言论的标准([来源](https://hatebase.org/faqs)):

*   它针对特定人群(种族、国籍、宗教、性别、残疾或阶级)；
*   有恶意；

仇恨言论有一个很难归类的主要问题:主观性。除了第一修正案的例外，仇恨言论没有法律定义，也不受法律制裁。因此，什么是仇恨言论，什么不是仇恨言论，可以有不同的解释。乔治·华盛顿大学的计算机科学研究员艾琳·卡莉斯坎认为，这在很大程度上取决于领域和语境。

但由于人类无法总是就什么可以被归类为仇恨言论达成一致，因此创建一个通用的机器学习算法来识别它就变得尤为复杂。此外，根据芬兰阿尔托大学的 Tommi grndahl 的说法，用于训练模型的数据集往往“反映了收集或标记数据的人的大多数观点”。

更复杂的是，即使对人类来说，也很难区分仇恨言论和攻击性语言。这就成了一个问题，尤其是当标签是由随机的用户根据他们自己的主观判断来做的时候，就像在[这个数据集](https://github.com/t-davidson/hate-speech-and-offensive-language/tree/master/data)中，用户被建议将推文标记为“仇恨言论”、“攻击性语言”或“都不是”。因此，在设计模型时，遵循有助于区分仇恨言论和攻击性语言的标准非常重要。

值得指出的是，Hatebase 的数据库在创建仇恨言论检测算法方面非常有用。这是一个多语种词汇，根据在仇恨言论中使用的可能性，这些词被贴上从“温和”到“极度冒犯”的标签。

尽管对于是否应该限制仇恨言论存在不同意见，但一些公司，如脸书、Twitter、Riot Games 和其他公司决定控制和限制仇恨言论，使用机器学习进行检测。

# 模型灵敏度

检测仇恨言论的另一个问题是机器学习算法对文本异常的敏感性。

模型是“用数据训练的算法的输出”([来源](https://www.toptal.com/machine-learning/ensemble-methods-machine-learning))。机器学习算法或模型可以为我们分类文本，但对微小的变化很敏感，比如删除令人讨厌的单词之间的空格。这一改变可以大大降低一个句子得到的负面分数([来源](https://www.wired.com/story/break-hate-speech-algorithm-try-love/))。学习模型可能会被愚弄，错误地标注它们的输入。机器学习算法的一个关键挑战是理解上下文。

仇恨言论的阴险本质在于，它可以根据上下文变化成许多不同的形态。如果社会对用词的选择达成共识，歧视性的想法可能隐藏在许多善意的话语中。例如，儿童玩具的名字和标签可以作为仇恨思想的绰号。在布尔逻辑中将意义归属于一个词的静态定义不具有适应为仇恨而改变昵称的灵活性。“人工智能在这一点上没有意识到语境，这就是语言令人憎恶的原因，”哈佛大学伯克曼·克莱恩互联网与社会中心的成员布里坦·海勒说。

每一家允许用户自行发布内容的公司都面临着一个挑战，那就是演讲与他们的品牌相关联。《连线》杂志 4 月刊描述了脸书的持续增长如何引发了一个重大问题，“该公司的商业模式是否与其宣称的使命(让世界更加紧密地联系在一起)相一致。”([来源](https://www.wired.com/story/facebook-mark-zuckerberg-15-months-of-fresh-hell/))仅仅通过给人们更多的工具来分享，我们可能无法让人们团结起来，让世界变得更美好。

在下一节中，我们将研究另一家公司 Riot Games 如何应对缓和仇恨言论的挑战。

# 案例分析:暴乱游戏的英雄联盟

![](img/81ac7f64a1bdaf6551639c9e6ab71a61.png)

对于那些不知道的人来说，英雄联盟是一个竞争性的游戏，两个队各有五名球员，试图摧毁对方的基地。

当然，在 2009 年发布时，Riot games 希望创造一个友好竞争能够蓬勃发展的有趣环境。这是最初的目标。

英雄联盟使用内置文本，随着游戏的普及和用户群的增长，竞争加剧。玩家开始使用聊天来幸灾乐祸他们在游戏中的表现，或者摧毁敌人团队阻止不可避免的失败的徒劳尝试。这仍然在公司的目标范围内。然而，很快，它就退化了，直到人们普遍看到这样的事情:“你的整个生活都是垃圾”，“自杀吧”，或者无数其他胜利者会对失败者做的下流事情的宣言。这变得如此平常，以至于玩家给它起了个名字:毒性。玩家变得麻木，甚至变得积极，正直的玩家会不假思索地做出有害的行为。Riot Games 发现，在他们的内部玩家分类(消极、中立和积极)中，87%的毒性来自中立或积极的玩家。疾病正在蔓延。([来源](https://www.gamesindustry.biz/articles/2015-07-08-homophobia-sexism-racism-reduced-to-2-percent-of-league-of-legends-matches))

2011 年，Riot Games 发布了一个名为“法庭”的解决方案。法庭被设计成与另一个游戏内的功能“报告”一起工作(“T2”来源)。在游戏结束时，如果你觉得另一个玩家中毒了，报告是将这些问题发送给 Riot Games 进行审查的一种方式。然后，Riot Games 会将报告交给法庭。该法庭是一个由志愿者组成的陪审团审判系统。担心的玩家可以注册法庭，然后查看游戏报告，并逐案投票决定某人是否真的有毒。如果你的投票与大多数人一致，你将获得少量游戏内货币，违规的有毒玩家将受到少量惩罚，对于屡犯者，惩罚将会增加。Riot Games 还向无毒玩家发放小额奖金。这些共同的努力使玩家群体得到了改善，Riot 发现，法庭的一项处罚就足以遏制大多数玩家的有害行为。

这个系统有两个主要问题:

1.  它既慢又低效。人工审查需要将这些聊天记录放到法庭网站上，然后必须等待足够多玩家的回应，然后在那里决定处罚。

2.它有时非常不准确(特别是在他们取消每次“成功”惩罚的奖励之前，这导致了系统中的超级先天偏见)。([来源](https://nexus.leagueoflegends.com/en-us/2018/08/ask-riot-will-tribunal-return/))

2014 年，暴乱导致法庭关闭。它已经工作了一段时间，但毒性仍然是一个问题。

**一个机器学习解决方案:**

然而，在那之后，Riot Games 获得了他们大约 1 亿份法庭报告([来源](https://www.gamesindustry.biz/articles/2015-07-08-homophobia-sexism-racism-reduced-to-2-percent-of-league-of-legends-matches))，并将其作为训练数据来创建一个机器学习系统，该系统可以检测出有问题的行为，并对这些行为做出定制化的回应(基于玩家在训练数据的法庭案件中的投票方式)。)

虽然法庭速度慢或效率低，有时需要几天或一两周才能做出判决(在玩家忘记他们的有毒行为很久之后)，但这个新系统可以在 15 分钟内分析并做出判决。玩家们几乎看到了他们行为的直接后果。

“由于这些治理系统改变了在线文化规范，英雄联盟中同性恋恐惧症、性别歧视和种族主义的发生率已经下降到所有游戏的 2%，”言语虐待下降了 40%以上，91.6%的负面玩家在一次报道的处罚后改变了他们的行为，再也没有犯下其他罪行。([来源](https://www.gamesindustry.biz/articles/2015-07-08-homophobia-sexism-racism-reduced-to-2-percent-of-league-of-legends-matches))

# 机器学习方法

机器学习方法在检测网络平台上的仇恨言论方面取得了突破。在本节中，我们将讨论一些传统上用于此任务的技术以及一些新方法。

**预处理数据**

自然语言处理(NLP)是将人类单词转换为机器可以理解的数字和向量的过程。人类世界和机器世界之间的一种工作方式。自然，这需要相当多的数据清理。通常，清理意味着删除停用词、词干化、标记化，以及实现词频-逆文档频率(TFIDF ),该词频赋予更重要的词比“the”之类的词更重的权重，而“the”之类的词因增加较少的含义而受到惩罚。([来源](https://medium.com/@ODSC/essential-nlp-tools-code-and-tips-39b7b2b7d7ba))词汇化是一种计算量更大的方法，用于提取单词的词干。([来源](https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html))

**模型实现**

一旦数据是干净的，我们使用几种方法进行分类。常见的文本分类方法有“情感分析、主题标注、语言检测、意图检测。”([来源](https://monkeylearn.com/text-classification/))更高级的工具包括朴素贝叶斯、bagging、boosting 和随机森林。每种方法都可以有一个召回率、精确度、准确度和 F1 分数，与它的分类程度相关联。然后我们要反复测试这些方法。尽管我们的人工智能在训练数据集上非常准确，但它们在测试数据上也同样糟糕。我们需要确保我们的模型不会过度适应我们的训练数据，使其在分类测试数据方面表现出色，但在准确分类未来数据方面表现不佳。下面是另外三种应对文本分类挑战的方法。

**多标签分类**

基线多标签分类方法，称为*二元相关性*方法，相当于为每个标签独立训练一个二元分类器([来源](https://en.wikipedia.org/wiki/Multi-label_classification))。这种方法将每个标签与其他标签分开处理。例如，如果你试图归类为“我讨厌那种食物，我们午餐不要吃它。”标签:午餐谈话，爱情谈话，仇恨谈话。您的分类器将遍历数据三次，每个标签一次。

对于下面的数据和标签，(预处理后)二元相关性方法将对每个标签进行单独预测。(我们将使用朴素贝叶斯分类器，在这里有很好的解释)

```
data = pd.read_csv('lunchHateLove.csv')
data.head()
```

![](img/c65a90ed48776dbeab067f844907cff1.png)

```
# using binary relevance
from skmultilearn.problem_transform import BinaryRelevance
from sklearn.naive_bayes import GaussianNB# initialize binary relevance multi-label classifier
# with a gaussian naive bayes base classifier
classifier = BinaryRelevance(GaussianNB())# train
classifier.fit(x_train, y_train)# predict
predictions = classifier.predict(x_test)#print the keywords derived from our text
#along with the labels we assigned, and then the final predictions
print(data.comment_text[1], '\n',
      data.comment_text[3], '\n',
      y_test, '\n',
      predictions, '\n') hate love kind food okay lunch 
food hate love get lunch 
    lunch_talk  love_talk  hate_talk
1        1          0          1
3        1          1          1 
  (0, 0)	1
  (1, 0)	1
  (1, 1)	1
  (0, 2)	1
  (1, 2)	1
```

因此，在这个简单的例子中，二元相关性预测第一列(0，0)中第一行的点对于标签“午餐 _ 谈话”是真实的，这是基于我们的原始输入的正确标签。事实上，在这个非常简单的例子中，二元相关性完美地预测了我们的标签。

如果你想更详细地了解这些步骤，这里有一个 Github 上这个例子的[链接](https://github.com/AlludedCrabb/Toy_Binary_relevance_Example/blob/master/Toy_Example_Binary_Relavance.ipynb)。或者更好的是，看看这个关于这个主题的[博客](/journey-to-the-center-of-multi-label-classification-384c40229bff)，它有更多的细节，还有一个到我用作起点的 Github 页面的链接。

**转移学习和监督不力**

机器学习模型的一个瓶颈是缺乏标记数据来训练我们识别仇恨言论的算法。两种解决方案是迁移学习和弱监督。

迁移学习意味着在新的任务中重用已经存在的模型，这不仅在缺少标记数据是一个问题的情况下，而且在未来可能需要重新标记时都非常有用。如果一个模型不是从零开始学习，而是从另一个为解决类似任务而设计的模型中学习，那么这个模型可以表现得更好，这种想法并不新鲜，但在 Fastai 的 [ULMFiT](http://nlp.fast.ai/classification/2018/05/15/introducting-ulmfit.html) 出现之前，它并没有在 NLP 中使用太多。

ULMFiT 是一种在数百万维基百科页面上使用预训练模型的方法，可以针对特定任务进行调整。这个调整后的模型稍后用于创建分类器。这种方法的效率令人印象深刻:*“仅用 100 个已标记的例子(并让它访问大约 50，000 个未标记的例子)，*【这是可能的】*实现与用 10，000 个已标记的例子从头训练一个模型相同的性能”* ( [来源](http://nlp.fast.ai/classification/2018/05/15/introducting-ulmfit.html))。另一个优点是，这种方法可以用于英语以外的语言，因为用于初始训练的数据来自许多语言的维基百科页面。其他一些用于 NLP 的迁移学习语言模型有:Transformer，Google 的 BERT，Transformer-XL，OpenAI 的 GPT-2，ELMo，Flair，StanfordNLP ( [source](https://www.analyticsvidhya.com/blog/2019/03/pretrained-models-get-started-nlp/) )。

在缺少标记数据的情况下，可以应用的另一个范例是弱监督，其中我们使用手写的启发式规则(“标签函数”)来创建可以应用的“弱标签”，而不是手动标记数据。在这个范例中，首先建立基于这些弱标签的生成模型，然后使用它来训练判别模型([源)](https://hazyresearch.github.io/snorkel/blog/weak_supervision.html)。

在本文的[中给出了使用这两种方法的例子。来自斯坦福大学的人工智能硕士生亚伯拉罕·斯塔罗斯塔(Abraham Starosta)展示了他如何结合使用弱监督和转移学习来识别反犹太人的推文。](/a-technique-for-building-nlp-classifiers-efficiently-with-transfer-learning-and-weak-supervision-a8e2f21ca9c8)

他从一组约 25000 条推文的未标记数据开始，并使用浮潜(一种用于弱监督标记的工具)通过编写简单的标签函数来创建训练集。这些函数用于训练“弱”标签模型，以便对这个大数据集进行分类。

为了将迁移学习应用于这个问题，他通过在一般化的推特上训练 ULMFiT 的语言模型，对其进行了微调。然后，他在用弱监督标签创建的训练集上训练这个新模型。结果相当令人印象深刻:作者能够达到 95%的精确度和 39%的召回率(概率阈值为 0.63)，而在不使用弱监督技术的情况下，对于 90%的精确度，召回率为 10%。该模型的表现也优于来自 sklearn、XGBoost 和前馈神经网络的逻辑回归(来源)。

**基于投票的分类**

基于投票的方法是用于分类的集成学习，有助于平衡单个分类器的弱点。集成方法结合了单独的分类器算法，例如:bagging(或 bootstrap aggregating)、决策树和 boosting。如果我们考虑一个线性回归或一条线来预测给定 x 的 y 值，我们可以看到线性模型不擅长识别非线性聚类。这就是集合方法的用武之地。“这种线性分类器集合的适当组合可以学习任何非线性边界。”([源](http://www.scholarpedia.org/article/Ensemble_learning))可以一起使用各自具有唯一判定边界的分类器。投票分类器的准确度“通常高于单个分类器”([来源](/ensemble-learning-in-machine-learning-getting-started-4ed85eb38e00)

我们可以通过多数投票(也称为简单投票、加权投票和最大投票)来组合分类器。在多数表决中，“分类系统遵循分而治之的方法，将数据空间划分为更小、更容易学习的分区，每个分类器只学习其中一个更简单的分区。”([来源](http://www.scholarpedia.org/article/Ensemble_learning))在加权投票中，我们可以多次统计更有用的模型。([来源](https://www.aclweb.org/anthology/Y07-1050))我们可以用这些方法对外文文本进行有效的分类。([来源](http://bit.ly/2wiZTpZ))就可用性而言，基于投票的方法有利于优化分类，但不容易解释。

意识到机器学习的强大应该伴随着对如何解决其局限性的理解。用于从我们的社交空间中删除仇恨言论的人工智能通常位于黑盒中。然而，随着对自然语言处理和文本分类的一些探索，我们可以开始解开我们对人工智能的期望，我们不需要成为科技巨头的一部分来永久实现分类器。