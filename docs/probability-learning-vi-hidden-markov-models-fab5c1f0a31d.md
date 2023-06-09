# 概率学习 VI:隐马尔可夫模型

> 原文：<https://towardsdatascience.com/probability-learning-vi-hidden-markov-models-fab5c1f0a31d?source=collection_archive---------1----------------------->

## 马尔可夫链和马尔可夫模型变得简单

![](img/8ff7f44a7780beb383492024191bda34.png)

**朋友们，你们好！**这是我们概率学习系列的第六篇文章，列出来是为了防止你错过之前的文章:

*   [概率学习一:**贝叶斯定理**](/probability-learning-i-bayes-theorem-708a4c02909a)
*   [概率学习二:**贝叶斯定理如何在机器学习中应用**](/probability-learning-ii-how-bayes-theorem-is-applied-in-machine-learning-bd747a960962)
*   [概率学习三:**最大似然**](/probability-learning-iii-maximum-likelihood-e78d5ebea80c)
*   [概率学习四:**贝叶斯**背后的数学](/probability-learning-iv-the-math-behind-bayes-bfb94ea03dd8)
*   [概率学习 V: **朴素贝叶斯**](/probability-learning-v-naive-bayes-7f1d0466f5f1)

我强烈建议你阅读它们，因为它们很有趣，充满了关于概率机器学习的有用信息。然而，如果你不想读它们，那绝对没问题，**这篇文章不需要通过一点概率知识就能理解。**

此外，不要担心，我不会在本文中包括任何复杂的数学:它的目的是**奠定隐马尔可夫模型的理论背景，展示如何使用它们，并谈论它的一些应用。**

我们已经见过 Bayes 牧师了，今天我们要去见另一个在博弈论和概率世界里非常有影响力的人。这不是别人，正是安德烈·马尔科夫，他把马尔可夫链放到隐马尔可夫模型中

隐马尔可夫模型是概率机器学习世界的一个分支，对于解决涉及处理序列的问题非常有用，如自然语言处理问题或时间序列。一会儿，我们会看到这是为什么，但首先，让我们了解一下马尔可夫。

*最后，在我们开始之前，这里有一些额外的资源可以让你的机器学习事业突飞猛进:*

```
*Awesome Machine Learning Resources:**- For* ***learning resources*** *go to* [***How to Learn Machine Learning***](https://howtolearnmachinelearning.com/books/machine-learning-books/)*! 
- For* ***professional******resources*** *(jobs, events, skill tests) go to* [***AIgents.co — A career community for Data Scientists & Machine Learning Engineers***](https://aigents.co/)***.***
```

# 这个安德烈·马尔科夫是谁？

![](img/e9b093992302a9b6b7aaddc0d2a40d6d.png)

Image of Andrei Markov

安德烈·马尔科夫(1856-1922)是一名俄罗斯数学家，在圣彼得堡大学教授概率论，同时也是一名非常活跃的政治人物。他研究了连续分数、中心极限定理和其他数学成果，然而，他最被人们铭记的是他在概率论方面的工作，特别是对随机过程的**研究**；我们一会儿将要讨论的马尔可夫链。

# 马尔可夫链:概率序列

让我们从马尔可夫提议的最基本元素开始:**马尔可夫链**。在概率论中，马尔可夫链或马尔可夫模型是一种特殊类型的离散随机过程，其中一个事件发生的概率仅取决于紧接在**之前的**事件。

潜在的假设是，给定现在，未来***独立于过去。换句话说，如果我们知道系统或变量的当前状态或值，我们不需要任何过去的信息来尝试预测未来的状态或值。***

![](img/3e5aea805b8e5b0357af4096fc687046.png)

Example of a two state Markov Chain

马尔可夫链通常由一组状态和每个状态之间的转移概率定义。在上面的例子中，显示了两个状态的马尔可夫链:我们有状态 A 和 B 以及四个转移概率:再次从 A 到 A，从 A 到 B，从 B 到 A，再次从 B 到 B。这些转移概率通常以矩阵的形式表示，称为**转移矩阵，也称为马尔可夫矩阵。**

![](img/0e285e333c1f8c50705535927bfe8c4d.png)

One possible transition matrix for this chain

**元素 *ij* 是从状态 j 过渡到状态 i** 的概率。在某些情况下，会使用转置符号，因此元素 *ij* 代表从状态 I 到状态 j 的概率。因此，我添加了‘to’和‘from’只是为了澄清。总的来说，该系统看起来像这样:

![](img/f140430402fc76eea72f7181e7b3a959.png)

Diagram of a Markov Chain with the transition probabilities

我们如何计算这些概率？这个答案你可能已经听过一百万次了:来自数据。

想象一下我们的马尔可夫链中的状态是晴天和雨天。为了计算从一个状态到另一个状态的转移概率，我们只需要收集一些代表我们想要解决的问题的数据，计算从一个状态到另一个状态的转移次数，并对测量结果进行归一化。下图显示了在我们的示例中如何实现这一点。

![](img/1ee9ce1afde2cc8916e611266436115b.png)

Calculations of transition probabilities from data

目前，马尔可夫链看起来就像任何其他的状态机，其中我们有状态和状态之间的转换。然而，在这篇文章的后面，我们将会看到它们是多么的特别。

好了，现在我们知道了什么是马尔可夫链，以及如何计算相关的转移概率，接下来我们继续学习隐马尔可夫模型。

# 隐马尔可夫模型:发现未知

隐马尔可夫模型是一种概率模型，它试图基于一些其他的 ***观察到的*变量**来找到具有某个值的某个 ***隐藏*变量**的值或概率。这些变量通常被称为隐藏状态和观察状态。

**一个系统的状态可能只是部分可观测的，或者根本不可观测**，我们可能不得不根据另一个完全可观测的系统或变量来推断其特征。

使用前面的示例，想象我们添加了以下信息。每天，我们都有可能接到住在不同大陆的最好的朋友约翰的电话，这种可能性取决于当天的天气情况。**利用后一种信息**(如果我们接到电话或没有接到电话- **观察变量** ) **我们想推断前一种信息**(约翰生活的大陆的天气-**隐藏变量**)

![](img/127a85274a24d2f65d3eb449573dae9b.png)

Hidden and observed variables for our problem

这里显示的概率定义了约翰在某一天给我们打电话的可能性，这取决于该天的天气，这些概率被称为 ***发射概率*** 。他们定义了在给定隐藏变量的某个值的情况下，看到某个被观察变量的概率。

知道了这些概率，加上我们之前计算的转移概率，以及隐变量的先验概率(有多可能是晴天或雨天)，我们就可以试着找出某段时间的天气，知道约翰在哪一天给我们打了电话。

让我们用简单的统计数据来看看如何解决这个问题:假设约翰连续两天没有给我们打电话。最有可能的天气情况是什么？**为此，我们首先需要计算先验概率**(即，在任何实际观测之前晴天或雨天的概率)**，这是我们从与转移概率相同的观测中获得的。**

![](img/90cbe9e5681c023401f2caf0090fc003.png)

Calculations of prior probabilities

现在，我们准备解决我们的问题:连续两天，我们没有得到一个迹象表明约翰还活着。那么最有可能的天气情况是什么？正如我们在下图中看到的，我们有 4 种可能的情况要考虑:晴天接着晴天，晴天接着下雨，下雨接着晴天，最后下雨接着下雨。

![](img/c486e3c1744dfb85cb9b23bd814c47f4.png)

Diagram of the process of calculating the probability for one weather scenario

在上图中，我们选择了第二个选项(晴天，然后下雨)，并使用先验概率(第一天在没有任何观测的情况下是晴天的概率)，从晴天到雨天的转换概率，以及在两种情况下没有接到电话的发射概率，**我们通过简单地乘以所有上述概率计算出了整个事件发生的概率。**

**我们将不得不为每一个可能的天气场景**(我们的例子中还剩 3 个)这样做，最后我们将选择一个产生最高概率的场景。(这叫做[最大似然估计，在我之前的一篇文章](/probability-learning-iii-maximum-likelihood-e78d5ebea80c)中有完整的描述)。

连续两天，我们必须计算四种可能的情况。三天之内，我们会有八个场景。一共四天十六天。如果我们想计算一整周的天气，我们将有 128 种不同的情况。随着可能情况的数量呈指数级增长，很容易看到这种情况会如何失控，从而促使我们使用更实用、更智能的技术。

这不仅是因为我们有更多的情景，而且在每一个情景中，我们都有更多的计算，因为在链条中有更多的转变和更多的排放概率。

**这就是马尔可夫链派上用场的地方。**

让我们刷新一下马尔可夫链的基本假设:**“*给定现在*，未来独立于过去”。**

知道了这一点，隐马尔可夫模型的操作原理是，它逐渐地**存储从长度 1 到 n-1** 的场景链的概率，n 是我们想要推断隐藏状态的链的长度，而不是计算许多不同场景的概率。

**这是什么意思？假设我们想在知道约翰给我们打电话的日子的情况下计算一整周的天气情况。为了计算最后一天的天气状况，我们将计算出那天是晴天的概率，给出通向晴天的最佳路径，对下雨的星期天做同样的事情，并只选择最高的一个。**

**这大大简化了前面的问题**。

![](img/2ae2e60a50eb8ef783e7dc3ee3be2518.png)

Intuition behind a Hidden Markov Model

递归地，为了计算周六晴天和雨天的概率，我们会做同样的事情，考虑减少一天的最佳路径。这意味着，在任何给定的一天，为了计算第二天可能的天气情况的概率，我们将只考虑在那一天达到的最好的概率——**没有先前的信息**。

![](img/82b1cef90784fc4f2ad42cc5b4b5b9fc.png)

At each given day we only use the BEST probabilities up to that day

在实践中，这是通过从第一时间步开始，计算观察隐藏状态的概率**并选择最佳状态**来完成的。然后，用那个最好的，我们在第二天做同样的事情，以此类推。让我们看看在我们的例子中是如何做到这一点的。

利用先验概率和排放概率，我们计算出第一天 T2 是晴天还是雨天的可能性。

![](img/0c20450930fbc05d7b8eb27c45434ea5.png)

Calculations of the probabilities of Monday being sunny and rainy

让我们看看第二天我们将如何继续:使用先前计算的晴天和雨天的最佳概率，我们将为第二天计算同样的概率，但是不使用我们上次使用的先验，**我们将使用晴天和雨天的最佳计算概率。**

为了做到这一点，我们首先来看看实际的观察结果是什么:假设星期一是晴天。那发生的概率是 0.375。现在，让我们来看看星期二是晴天:我们必须将星期一是晴天的概率乘以从晴天到晴天的转换概率，乘以晴天没有被约翰打电话的排放概率。这给了我们一个概率值 0，1575。

![](img/83ec9d7b7c04681f91fea90d713f4886.png)

Calculations of probabilities of sunny and rainy for Tuesday

现在，假设星期一下雨。星期二是晴天的可能性有多大？为此，我们将周一下雨的最高概率(0.075)乘以从下雨到晴天的转换概率(0.4)乘以晴天且没有接到电话的排放概率，就像上次一样。这导致概率为 0.018，并且因为我们计算的前一个(周一晴和周二晴)更高(它是 0.1575)，我们将保留前一个。

我们现在必须为一个多雨的星期二做同样的事情，保持两个计算概率中的最高值。**如果我们继续这个链条，现在计算周三的概率**:

![](img/6d8207036fe328defe77779d2ef9b76f.png)

Calculations of probabilities for Wednesday

如果我们对整个星期都这样做，我们会得到七天中最可能的天气情况，如下图所示:

![](img/565c916f7eea1ffa1a21c3c01bba5c7a.png)

Weather conditions for the whole week

通过这个过程，我们可以推断出任何时间段最可能的天气情况，只需知道 John 是否给我们打过电话，以及来自历史数据的一些先验信息。

**就是它！现在你已经知道了隐马尔可夫模型背后的基本原理，让我们看看它的一些实际应用。**

# **隐马尔可夫模型:应用**

*如前所述，hmm***在处理序列时非常出色。**正因为如此，它们在**自然语言处理**中被广泛使用，在这里短语可以被认为是单词序列。

hmm 用于许多 NLP 应用程序，但是让我们举几个具体的例子来巩固您头脑中的想法。

论文[*使用统计方法的实时在线无约束手写识别*](https://ieeexplore.ieee.org/document/480098) 讲述了使用 HMMs 将手写文档翻译成数字文本的**。**

我手机上有一个名为“钢笔打印”的应用程序，就是做这个的。它将手写文本作为输入，将其分解成不同的行，然后将整个内容转换成数字格式。下图显示了这样一个例子。

![](img/1edff113472ee483d58e98c0f658a573.png)

Pipeline of the Pen to Print app

有很多这样的应用程序，大多数时候它们使用一些概率方法，比如我们看到的隐马尔可夫模型。

另一篇论文， [*为基于 HMM 的语音合成考虑全局方差的语音参数序列建模*](https://www.intechopen.com/books/hidden-markov-models-theory-and-applications/modeling-of-speech-parameter-sequence-considering-global-variance-for-hmm-based-speech-synthesis) 做了类似的事情，但是用语音代替文本。

我认为，我们所有的虚拟助手，如 Siri、Alexa、Cortana 等，都是在以下过程中工作的:你用某种行动号召短语唤醒他们，他们开始积极倾听(或者他们是这么说的)。在这之后，你说的任何话，比如对某种音乐的请求，都会被麦克风拾取并从语音翻译成文本。然后这些文本被处理，我们得到想要的输出。

hmm 的其他用途包括从[计算生物学](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5172443/#bib36)到在线营销或为在线商店发现购买因果关系。

# 结论

我们已经看到了什么是隐马尔可夫模型，以及它们被用来解决实际问题的各种应用。未来会有更多概率学习的帖子，请关注我的[](https://medium.com/@jaimezornoza)**，敬请关注！**

**就这些，我希望你喜欢这个帖子。请随时在 LinkedIn 上与我联系，或者在 Twitter 上关注我，地址是:jaimezorno。还有，你可以看看我其他关于数据科学和机器学习的帖子[**这里**](https://medium.com/@jaimezornoza) 。好好读！**

# **额外资源**

**如果你想了解更多一点，从这篇文章中澄清你的学习，或者深入 HMMs 的数学，我在这里留下了一些我认为可能会很有用的信息。**

*   **[马尔可夫链的精彩互动讲解](http://setosa.io/ev/markov-chains/)**
*   **[关于隐马尔可夫模型的 Youtube 视频](https://www.youtube.com/watch?v=kqSzLo9fenk)**
*   **[描述 HMMs 背后的数学原理的中等帖子](https://medium.com/@jonathan_hui/machine-learning-hidden-markov-model-hmm-31660d217a61)**
*   **[最好的统计与概率课程回顾](https://howtolearnmachinelearning.com/online-courses/statistics-and-probability-courses/)。**

***有关机器学习和数据科学的更多资源，请查看以下资源库:* [*如何学习机器学习*](https://howtolearnmachinelearning.com/books/machine-learning-books/) *！有关职业资源(工作、事件、技能测试)，请访问*[*AIgents.co——数据科学家职业社区&机器学习工程师*](https://aigents.co/) *。***

**请尽情享受，如有任何疑问，请随时联系我！**