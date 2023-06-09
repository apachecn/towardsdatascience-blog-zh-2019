# 对话式人工智能中的种族主义

> 原文：<https://towardsdatascience.com/racial-bias-in-conversational-artificial-intelligence-be0d3abd9b39?source=collection_archive---------16----------------------->

![](img/f005cdd3ef4f07582e1e7e2d38a3e7b9.png)

Racial Bias in Conversational AI ([source](https://www.technologyreview.com/s/609338/new-research-aims-to-solve-the-problem-of-ai-bias-in-black-box-algorithms/))

**什么是对话式人工智能**

这是一个新兴的人机交互领域，我们使用自然语言来交换信息并向计算机传递命令。你能想到的任何与数字设备的单一界面都可以被人工智能支持的对话界面取代或增强。例子包括聊天机器人&基于语音的助手，如 Siri。

现代智能城市概念还涉及“以公民为中心”的服务模型，该模型使用对话式人工智能界面来个性化和情境化城市服务。一个例子是公民参与平台 [Citibot](https://www.citibot.io/) 。同样，维也纳有一个 WienBot，让居民和游客可以找到常见的市政服务，如找到停车场、洗手间、餐厅和其他设施。他们不再需要依赖陌生人的善意，或者在网站上浏览长长的名单。

![](img/682b8b64ee0f94b2f6d222414f929ee5.png)

Virtual AI assistants ([source](https://smsbits.in/blog/2018/04/17/chat-bots-vs-human-assistance/))

**问题:对话式人工智能和人类一样有偏见**

聊天机器人使用复杂的算法，通过数百万个例子进行学习。如此大规模的语言数据只存在于新闻文章和社交媒体等公共数据源中。通过使用未经检查的公共数据，人工智能可以包含人类最糟糕的特征，并最终体现社会的偏见。垃圾入垃圾出的老编程原则在这里适用。让我们看看这个问题的几个经典例子。

**微软与人工智能聊天机器人的斗争**

2016 年 3 月，微软推出了 TAY(一个 twitter 机器人)，作为对话式人工智能的实验。这个聊天机器人在 twitter 上与公众互动，从对话中学习并发布消息。人类互动不到 24 小时就腐蚀了一个无辜的 AI 聊天机器人。下面可以看到该机器人发出的一些令人无法接受的推文。

![](img/e49ce36139b20e17a051f8c5d72fc291.png)![](img/0280d19e1e579252d805713368989671.png)

ZO 是 TAY 的温和版，由微软于 2017 年夏天发布。它被塑造成不讨论政治和宗教，并避免参与种族和不适当的谈话。下图显示了其对争议话题的回应示例。这看起来做得不错，但有一个缺陷，我将在下一节强调。

![](img/216d3bfdedf74620986455a6f628951b.png)

Zo reacts to controversial topics ([source](https://qz.com/1340990/microsofts-politically-correct-chat-bot-is-even-worse-than-its-racist-one/))

**没有上下文的审查**

Zo 对一系列广泛话题的不妥协态度是人工智能中一个令人不安的趋势:没有背景的审查。Zo 没有推断语言上的细微差别和上下文，只是回避了黑名单上的术语。这可能会导致股权问题，如下图所示。一些开源黑名单库被维护，虚拟对话代理使用它们来避免某些对话。令人惊讶的是，我发现其中一个开源库在某个时候在黑名单库中出现了我的国家“巴基斯坦”的名字([链接](http://tinysubversions.com/2013/09/new-npm-package-for-bot-makers-wordfilter/))。如果这些代理被部署在城市环境中提供服务，这可能导致公平、包容和拒绝服务的问题。

![](img/8c9971eb7669a9b5762a10dfe46528b4.png)

Censorship without context ([source](https://qz.com/1340990/microsofts-politically-correct-chat-bot-is-even-worse-than-its-racist-one/))

**一个小实验**

神经语言模型是虚拟语音助手的重要组成部分。一旦经过训练，它可以通过分配概率来计算哪些句子更有可能被说出。我在公开的新闻数据上训练了一个语言模型，并用一种简单的技术进行了种族审计。我使用的数据集由标题中含有犯罪一词的新闻文章组成。

![](img/730b5c89f0262cf7d700b4f7ea60d88a.png)

我通过比较与不同种族群体相关的否定句的概率，对我的模型进行了种族审核。这种基于模板的因果测试技术已经被使用，这在[最近的研究](https://aclweb.org/anthology/S18-2005.pdf)中有所体现，用于从神经网络模型中测量社会偏见。

![](img/cc6e15408d6f41e643339a5af381af97.png)

这里显示的概率是一个标准化的(条件)概率，它可以被解释为产生这些句子之一的句子的概率。可以观察到，在种族身份之间存在巨大的歧视，因为 model 从新闻数据中学习犯罪统计，并且这很可能在生成的文本中表现出来。github 上有代码。

[](https://github.com/muaz-urwa/Racial-Bias-in-Coversational-AI) [## muaz-urwa/转变中的种族偏见

### 通过在 GitHub 上创建一个帐户，为 muaz-urwa/种族偏见转化人工智能的发展做出贡献。

github.com](https://github.com/muaz-urwa/Racial-Bias-in-Coversational-AI) 

**原始影响评估**

Gartner 预测，到 2022 年，30%的客户体验将由对话代理处理，而 2017 年仅为 3%。[1]超过 60%的纽约市居民是非白人。[2]假设上述信息是正确的，并且所有种族都同样可能使用对话人工智能，对于纽约市，我们正在讨论纽约市(0.3 x 60) 20%的公平和包容。

**解决方案**

社会偏见正在引起 NLP 社区的关注，已经有一系列好的出版物试图解决单词嵌入和下游任务(如情感分析和共同引用解析)中的性别偏见问题。但是种族偏见是一个相对困难的问题，在好的去偏见技术方面还没有足够的进展。在公共决策中的一般人工智能应用的问责制方面已经有了发展，但据我所知，在对话式人工智能的问责制方面还没有这样的进展。算法影响评估是一种算法问责框架，由 NYU 的研究机构 AI Now 提出，旨在让公共机构对其自动化决策负责。我希望看到他们在框架中包括对话式人工智能的种族审计。