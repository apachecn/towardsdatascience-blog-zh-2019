# 适合初学者的 Tweepy

> 原文：<https://towardsdatascience.com/tweepy-for-beginners-24baf21f2c25?source=collection_archive---------8----------------------->

## 使用 Twitter 的 API 建立你自己的数据集

![](img/6ff04bdf429a306edd6fe07d23be0330.png)

建立你的投资组合的一个好方法是自然语言处理项目，但是像每个项目一样，第一步是获取数据。Twitter 可以成为文本数据的巨大资源；它有一个 API，凭证很容易获得，并且有许多 python 库可以帮助调用 Twitter 的 API。

总的来说，这些资源很棒，但它们有一些容易引起头痛的怪癖，本文将帮助您导航该过程并避免这些头痛，请将它视为您的赛前扑热息痛！

## 第一步:获得你的证书

**给自己注册一个账户:**Twitter 用户账户是拥有“开发者”账户的必要条件，所以要么注册一个新账户，要么登录一个现有账户。

**申请开发者账号:**前往[https://developer.twitter.com](https://developer.twitter.com/)申请开发者账号。如果出现提示，请选择个人或个人帐户，而不是企业帐户。当提交一个预期用途时，确保你的答案是足够描述性的，而不是一些垃圾或现成的复制粘贴语句。

**创建 app:** 在[https://developer.twitter.com/en/apps](https://developer.twitter.com/en/apps)注册 app。对于必填的网站字段，您可以放置一个占位符。设置完成后，转到“令牌和密钥”以生成访问令牌和密码。连同消费者 API 密钥(已经生成)，这些是我们用来与 Twitter API 通信的凭证。

## 步骤 2:安装 Tweepy

有几个库可用于与 Twitter 的 API 交互，我更喜欢 [Tweepy](https://tweepy.readthedocs.io/en/latest/) ，它进行可靠的调用，非常适合处理超过 140 个字符的推文。

只需将`pip install tweepy`写入您的终端。

您可能需要的其他几个库(取决于您想做什么)是 json、pandas、time 和 datetime。稍后我们会看到更多关于这些的内容。

## **第三步:快速测试运行**

API 凭证，检查。Tweepy 安装完毕，检查完毕。时间来看看它是否工作，粘贴下面的代码在一个笔记本上，在你自己的键 sub(注意错别字！)然后跑。

嘣！您刚刚进行了第一次 Twitter API 调用。你现在应该会看到你的账户主页时间线上的一系列推文(你的账户关注的每个人的推文)。它看起来会像这样:

![](img/248972ff4351d84f337c1e45ccad9acf.png)

Tweepy text output

够简单了吧？不对。我们可能会看到一些数据，但在目前的格式下，这些数据不是很有用，一些推文已经被截断，我们只有来自我们已经关注的账户的数据。如果我们想要构建一个结构化的数据集来进行分析，我们必须更深入地研究 API 调用输出…戴上安全帽！

## 步骤 4:检查 tweets json

在一个新的单元格中键入并执行`public_tweets[0]`来查看与第一条 tweet 相关的 json，享受输出。

![](img/b3195249df47a19353759638fcad4426.png)

A messy output, hard to make sense off

这不是我们处理数据的方法，试几分钟，你就会重读几行，然后马上让自己头疼。

如果你以前尝试过抓取，你可能使用过 [pprint](https://docs.python.org/3/library/pprint.html) (漂亮的打印)以一种更可读的方式格式化数据。不幸的是，pretty print 在这里不能帮助我们，因为 public_tweets[0]不是一个基本的 python 数据类型，它的类型是 tweepy.models.Status，并且 pprint 模块不兼容。

我们需要使 tweepy 的输出更具可读性，这样我们就可以知道需要编写什么代码来提取我们想要的数据。我们可以这样做:

现在，您将看到一些更有条理的东西:

![](img/df2d333cd2508e6ad9782c3a8bb54f30.png)

A clean output, a lot easier to parse

有了这个视图，我们可以慢慢地浏览字典和列表，以确定哪些信息是可用的，以及访问这些信息需要哪些键。

## 步骤 5:解析出数据

如果您只是想要 tweet 上的原始数据(文本、id、用户 id)，访问这些信息相对容易和可靠，正如我们已经看到的，当使用 home timeline API 调用时，我们可以使用`status.text`访问 tweet 的文本。

根据你项目的性质和你需要的数据，你需要选择[合适的 API 调用](https://tweepy.readthedocs.io/en/latest/api.html#tweepy-api-twitter-api-wrapper)来收集它。本文的其余部分将重点介绍如何使用 [user_timeline 调用](https://tweepy.readthedocs.io/en/latest/api.html#API.user_timeline)，该调用(对于一个标准帐户)可以检索一个用户的多达 3200 条最新推文(只要配置文件没有被锁定)。

这就是 Tweepy 变得有点麻烦的地方。API 调用返回的 json 结构根据 tweet 的特征而变化(想想常规 tweet、retweet 或 quote tweet)。不是提供一致的格式(如果没有信息可用，则键指向空列表)，有些键只在有数据指向时才出现。

克服这一点的简单方法是满足于主要的推文信息，但是如果你关心转发和引用，那么你的数据将是不完整的。如果我们想要构建一个丰富的数据集，我们需要使用 try 和 except 语句来处理这种不一致性。

收集数据的一个好方法是构建一个可以进行 API 调用并一次性解析数据的类。它可能看起来像这样:

关于这段代码的几点说明:

*   无论 tweet 类型如何，挖掘的字典中没有 try 语句的所有内容都是可访问的。
*   `tweet_mode = 'extended'`将文本索引替换为 full_text，并防止长度超过 140 个字符的主要推文被截断。不幸的是，转发仍然被截断，我们可以使用`.retweeted_status.full_text`访问完整的转发文本，这里我们放入一个 try 语句，因为它只在推文是真正的转发时出现。
*   位置数据包含坐标、城市和国家，这取决于您想要什么，您需要进一步解析它，但这很容易。
*   result_limit 和 max_pages 相乘得到调用的 tweets 数。
*   转发和引用推文包括在你的 3200 条推文中，无论你是否收集它们(关闭此设置不会获得更多主推文)。
*   如果你在使用这个类打电话时没有提供用户名，你将会从独一无二的 [wint](https://twitter.com/dril) 中抓取推文，欢迎你！

请务必花时间对照我们之前制作的结构化 json 输出版本和两个附加输出(每种 tweet 类型一个，常规、转发和引用)来查看这段代码。通过这样做，你将更好地理解数据是如何被访问的，并准备好为[不同的调用](https://tweepy.readthedocs.io/en/latest/api.html#tweepy-api-twitter-api-wrapper)创建你自己的类，或者修改这个类来收集额外的数据。

## 第六步:选择一个项目，确定你想要的数据

这可能是你的第一步，甚至可能是你读到这篇文章的原因。在这里你可能不需要太多帮助，但是一些建议不会有坏处。

在开始一个项目之前，找出是否有任何可用的现有资源。像每一个原始数据科学家一样，我带着分析政客的推文的意图选择了 Tweepy，通过快速的谷歌搜索，我找到了每一个拥有推特账户的英国国会议员的推特账号列表，这让我省去了很多繁重的工作。

明确你的目标，如果是学习，确保你关注其他项目，这有利于激励，获得想法，如果你陷入困境，可以帮助你指出正确的方向。如果原创是你的目标，再次，看看其他项目，你最好的想法可能是对现有项目的补充，拥抱开源哲学。

一旦你确定了你想收集谁的 tweets，就把所有的句柄收集到一个字符串列表中(不要在每个 Twitter 用户名前加上@符号)。

## 步骤 7:收集数据！

通过导入所需的库来启动会话:

复制该类的代码，代入您自己的 API 凭据。

实例化您的 miner，记住默认的 tweets collected 设置为 20，您可以在实例化时更改它(调用时指定的页面数量，即调用收集的 result_limit 的倍数):

现在，您已经准备好打电话，并以您可以使用的格式收集数据。要拨打电话:

现在你知道了。有了 3200 条 [wint](https://twitter.com/dril) tweets 的数据框架，你离理解生命的意义就差一点点了！

最后要记住的是 API 调用是有限制的，对于一个标准用户来说，这是每 15 分钟 900 个请求。不要担心，一条 tweet 不是一个请求，但是可能很难知道你什么时候要过去。要同时拨打多个电话，请尝试以下方法:

开始在没有睡眠计时器的情况下打电话，然后如果你得到一个与你的通话限制有关的错误，就试试睡眠计时器和计数器 if 语句(每 25 次通话启动一次计时器)，直到你得到对你有用的东西。

最后，注意 all_tweets 数据帧的索引对于每个句柄都是重复的。为了使它对所有的推文都是唯一的，需要重新设置索引。

就这些了！你现在已经准备好以一种可用的格式收集大量的推文了。狩猎愉快！