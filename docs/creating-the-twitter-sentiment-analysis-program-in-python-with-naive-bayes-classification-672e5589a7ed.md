# 用 Python 和朴素贝叶斯分类创建一个 Twitter 情感分析程序

> 原文：<https://towardsdatascience.com/creating-the-twitter-sentiment-analysis-program-in-python-with-naive-bayes-classification-672e5589a7ed?source=collection_archive---------0----------------------->

![](img/edb60e6eb2b628eed30e9e9f08a77a67.png)

Photo by [Hello I'm Nik](https://unsplash.com/@helloimnik?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你在科技领域呆得够久，你一定听说过情绪分析这个术语。它是预测一条信息(最常见的是文本)是否表明对该主题的积极、消极或中性情绪的过程。在这篇文章中，我们将通过制作一个 Python 程序来分析关于特定主题的推文的情感。用户将能够输入一个关键字，并根据包含输入关键字的最新 100 条推文获得对它的看法。

# 情感分析简介

也被称为“观点挖掘”，*情感分析*指的是使用自然语言处理来确定在线提及中的发言者、作者或其他主题的态度、观点和情绪。

> 本质上，它是决定一篇文章是正面还是负面的过程。这也叫内容的极性。

作为人类，我们能够下意识地将文本分为正面/负面。例如，句子“这个孩子脸上有一个灿烂的笑容”，最有可能给我们一个积极的情绪。用外行人的话来说，我们通过检查单词并平均正面和负面来得出这样的结论。例如，单词“华丽”和“微笑”更可能是积极的，而单词“the”、“kid”和“face”实际上是中性的。因此，句子的整体情绪很可能是积极的。

这项技术的一个常见用途是将其部署在社交媒体领域，以发现人们对某些话题的感受，特别是通过用户在文本帖子中的口碑，或者在 Twitter 的背景下，他们的*推文*。

# 先决条件

*   基本编程知识:

虽然 Python 在这个迷你项目中的参与度很高，但并不要求对该语言有很深的了解，只要你有基本的编程知识就可以了。

*   安装的工具:

对于这个程序，我们需要在计算机上安装 Python。我们将使用库`twitter`、`nltk`、`re`、`csv`、`time`和`json`。您可能必须安装前两个库。其余的已经随 Python 解释器一起提供了。不过，检查它们是否是最新的也无妨。

*   数据集分割概念:

这对于全面了解流程管道至关重要。你只需要知道[训练和测试数据集](https://medium.com/datadriveninvestor/what-are-training-validation-and-test-data-sets-in-machine-learning-d1dd1ab09bae)之间的区别，以及每一个在什么样的上下文中使用。

*   基本的 RESTful API 知识:

这并不重要，但会有所帮助。我们将在代码中到处使用 Twitter API，对 API 进行正常调用，并处理它返回的 JSON 对象。如果你需要，你可以在这里找到官方的 Twitter API 文档。

# 生产过程说明

**A 区:准备测试集**

*   步骤 A.1:获取身份验证凭据
*   步骤 A.2:认证我们的 Python 脚本
*   步骤 A.3:创建构建测试集的函数

**B 区:准备训练集**

**C 部分:预处理数据集中的推文**

**D 部分:朴素贝叶斯分类器**

*   步骤 D.1:建立词汇
*   步骤 D.2:根据我们的词汇匹配推文
*   步骤 D.3:构建我们的特征向量
*   步骤 D.4:训练分类器

**E 部分:测试模型**

# 在我们开始之前:

*   Twitter 有时需要几天时间来批准您的应用程序使用 Twitter API。然而，它通常需要不到 24 小时。
*   下载训练集可能需要 10 多个小时(这将在后面解释)。
*   教程摘自 Udemy 课程:[从 0 到 1:机器学习、NLP、Python——开门见山。](https://www.udemy.com/from-0-1-machine-learning/)

# A 部分:准备测试集

因为我们的情感分析的任务主要集中在文本数据上，所以会有大量的文本处理。这肯定是正确的。事实上，我们的测试和训练数据将仅仅由文本组成。

我选择从测试集开始，是为了让大家为训练集提取部分做好准备，因为它更依赖于 API。下面是我们将要做的事情的一点概述:

> 1-注册 Twitter 应用程序以获得我们自己的凭证。
> 
> 2-使用凭证通过 API 验证我们的 Python 脚本。
> 
> 3-创建基于搜索关键字下载推文的功能。

向 Twitter 注册应用程序至关重要，因为这是获得认证凭证的唯一途径。我们一拿到证书，就开始写代码。步骤 3 是测试集所在的地方。我们将根据我们试图分析情绪的术语下载推文。

**步骤 A.1:获取认证凭证**

首先，我们需要访问 Twitter 开发者网站，并通过以下链接登录我们的帐户:

 [## Twitter 开发者平台

### Twitter 是世界上企业和个人联系的最佳场所。自从早期的 Twitter 人…

developer.twitter.com](https://developer.twitter.com/content/developer-twitter/en.html) 

在右上角，点击应用程序按钮，创建一个应用程序，应用，然后继续，如下所示:

![](img/4df2b3df0eacd57f4f6fdbf34efd2ee5.png)

接下来，我们将选择“我请求访问供我个人使用”选项:

![](img/effb7bd430c11edc4a3bdbd673e68819.png)

在同一个网页上，向下滚动一点，输入您的帐户名称和国家/地区，然后单击继续，您将被重定向到下一个网页。在这里，您可以选择任何您感兴趣的用例。对于我们的案例，我选择了以下内容:

![](img/c800854f9c65e5697e3fff0b3961036e.png)

做出选择后，向下滚动并填写所需的用例兴趣段落。Twitter 现在非常重视这一点(我猜他们从脸书的错误 xD 中吸取了教训)，所以确保你强调该应用程序是一个自学/学术相关的项目。政府参与问题选择“否”，按“继续”。

在下一个网页上，阅读条款和条件列表，同意他们，然后提交申请。

接下来，打开您的电子邮件，通过发送给您的电子邮件中包含的链接验证您的 Twitter 开发人员帐户。最后，您将收到类似以下内容的消息:

![](img/a2c8156a2b61c27986c273843c26a1e7.png)

你现在能做的就是等待几个小时，让申请获得批准(如果你的解释没有违反 Twitter 的条款和条件，几乎肯定会获得批准)。

当您收到批准电子邮件时，单击其中包含的登录链接。您将被重定向到以下网页，在这里您应该选择“创建应用程序”:

![](img/7a9de9017c34dba3584cb1a943d8ca7b.png)

在下一个网页上，点击右上角的“创建应用程序”。重定向后，填写所需的应用程序详细信息，包括——如果你愿意——这是为了自学。点击“创建”。

下一个网页将包括您刚才输入的应用程序详细信息、访问令牌和权限。进入“密钥和令牌”选项卡。将 API 密匙和 API 秘密密匙复制到一个安全的地方(如果你愿意的话，可以是一个文本文件)，因为我们稍后会用到它们。

![](img/71ae5903213c6280dc0f3a895e629df5.png)

完成所有设置后，单击“创建”以生成访问令牌凭证。将访问令牌和访问令牌密码也复制到一个安全的地方。我们已经完成了凭证获取部分！

**步骤 A.2:认证我们的 Python 脚本**

既然我们现在有了 Twitter 开发人员的登录凭证(即 API 密钥和访问令牌)，我们就可以继续认证我们的程序了。首先，我们需要导入 Twitter 库，然后创建一个 Twitter。API 对象和我们讨论过的“安全”位置的凭证，如下所示:

前面代码片段中的最后一行只是为了验证我们的 API 实例是否工作。这将根据我们得到的输出来确定。运行上面的代码，您应该得到类似下面的 JSON 响应:

```
{"created_at": "Tue Feb 12 17:48:27 +0800 2019" 'default_profile": true ............} 
```

这没什么疯狂的，只是一些关于通过你的 Twitter 账户访问 API 的数据。如果你到了这里，你就可以走了。

**步骤 A.3:创建构建测试集的函数**

现在，我们可以开始创建一个函数来下载我们讨论过的测试集。基本上，这将是一个函数，以搜索关键字(即字符串)作为输入，搜索包含该关键字的推文，并将它们作为 twitter 返回。我们可以迭代的状态对象。

> 不过，这里需要注意的是，出于安全考虑，Twitter 限制了通过 API 发出请求的数量。此限制为每 15 分钟窗口 180 个请求。

这意味着，我们每 15 分钟只能使用我们的搜索功能获得多达 180 条推文，这应该不是问题，因为我们的训练集无论如何都不会那么大。为了简单起见，我们现在将搜索限制在 100 条 tweets，不超过允许的请求数。我们搜索推文(即测试集)的功能是:

正如您所料，这个函数将返回包含我们的搜索关键字的 tweets 列表。

> 请注意，我们将每条 tweet 的文本都耦合到了一个 JSON 对象中，标签目前为空。这仅仅是因为我们稍后会将每条推文分类为正面或负面，以便根据多数计数来确定对搜索词的情绪是正面还是负面。这就是情感分析的实际工作方式。

在我们继续之前，让我们通过在函数体后面添加以下代码来测试我们的函数:

这应该会在您的 IDE 终端上打印出五条包含我们的搜索关键字的 tweets(如果您正在使用的话)。现在一切都准备好了。我们有了测试集，可以继续构建我们的训练集了。

# B 部分:准备训练集

注意，到目前为止，我们还没有写很多代码。这要归功于 Python 简洁的语法之美，以及外部程序就绪库的使用，比如 RESTful APIs(在我们的例子中是 Twitter API)。

在这一节中，我们还将使用上一节中的 Twitter API 实例。然而，我们需要先解决一些事情。我们将使用可下载的训练集。根据内容的不同，这些微博都被标上了正面或负面的标签。这正是训练集的用途。

> 训练集对模型的成功至关重要。数据需要正确标记，不能有不一致或不完整的地方，因为培训很大程度上依赖于这些数据的准确性和获取方式。

对于这项任务，我们将使用令人惊叹的 Niek Sanders 的超过 5000 条手动分类推文的语料库，这使得它非常可靠。这里还有一个问题。Twitter 不允许在个人设备上存储推文，尽管所有这些数据都是公开的。因此，语料库包括每个 tweet 的关键字(tweet 的主题)、标签(pos/neg)和 tweet ID 号(即我们的 CSV 语料库中的行)。你可以从[原始站点](http://www.sananalytics.com/lab/twitter-sentiment/)获得包含语料库的文件，或者通过[个人知识库](https://github.com/karanluthra/twitter-sentiment-training/blob/master/corpus.csv)的这个链接。

让我们往回走一点。还记得我们说过的 Twitter API 限制吗？这也适用于这里，因为我们将使用 API 通过语料库中包含的每个 tweet 的 ID 号来获取实际的 tweet 文本。这意味着，要下载 5000 条推文，我们需要遵循:

```
max_number_of_requests = 180
time_window = 15 minutes = 900 secondsTherefore, the process should follow:Repeat until end-of-file: {
    180 requests -> (900/180) sec wait
}
```

现在，让我们编写代码来实现这一点。让我们不要忘记将通过 API 获取的 tweets 保存到一个新的 CSV 文件中，这样我们就不必在每次运行代码时都下载它们。我们的职能如下:

这很难，但是如果我们把它分解成几个部分，就相当简单了。首先，我们定义函数来接受两个输入，这两个输入都是文件路径:

*   `corpusFile`是我们下载的 Niek Sanders 的 CSV 语料库文件的字符串路径。如前所述，这个文件包括 tweet 的主题、标签和 id。
*   `tweetDataFile`是我们想要保存完整推文的文件的字符串路径。与`corpusFile`不同，这个文件将包括每条推文的文本以及主题、标签和 id。

接下来，我们从一个空单`corpus`开始。然后我们打开文件`corpusFile`，将文件中的每条推文添加到列表`corpus`。

代码的下一部分处理基于 id 获取 tweets 的文本。我们循环遍历 corpus 中的 tweet，调用每个 Tweet 上的 API 来获取 Tweet。特定推文的状态对象。然后，我们使用同一个对象(`status`)获取与之相关的文本，并将其推入`trainingDataSet`，然后休眠(即暂停执行)五分钟(900/180 秒)，以遵守我们讨论过的请求限制。

现在让我们花点时间离开我们的脚本，在最后一个函数之后下载推文(这将花费几个小时)。我们可以使用下面的代码片段来做到这一点:

代码一执行完，您的`tweetDataFile` CSV 文件就会充满 tweets(事实上大约 5000)。如果你走到这一步，恭喜你！—我第一次花了很长时间才顺利到达这里。现在我们完成了相对无聊的部分。让我们为即将到来的部分做好准备。

# C 部分:在数据集中预处理推文

在我们进入实际的分类部分之前，有一些清理工作要做。事实上，这一步非常关键，在建立机器学习模型时通常需要很长时间。然而，这在我们的任务中不是问题，因为我们拥有的数据是相对一致的。换句话说，我们确切地知道我们需要从它那里得到什么。我稍后会就此事发表意见。

下面说说情感分析中什么重要，什么不重要。单词是最重要的部分(在某种程度上，我们将在接下来的部分中讨论)。然而，当涉及到标点符号之类的东西时，你无法从标点符号中获得情感。所以标点对情感分析来说无所谓。此外，图片、视频、网址、用户名、表情符号等推文组件。不要助长推文的极性(无论是正面还是负面)。然而，这只适用于这个应用程序。例如，在另一个应用程序中，你可以有一个[深度学习](/how-does-back-propagation-in-artificial-neural-networks-work-c7cad873ea7)图像分类器，它学习并预测推文中包含的图像是代表积极的东西(例如彩虹)还是消极的东西(例如坦克)。说到技术性，情感分析和深度学习都属于机器学习。事实上，你可以通过深度学习进行情感分析，但那是另外一个故事了。

因此，我们知道我们需要在现有的推文中保留什么，需要去掉什么。这适用于训练集和测试集。因此，让我们创建一个预处理器类:

这很难，所以让我们把它分成几部分。我们从导入的库开始。`re`是 Python 的正则表达式(RegEx)库，它负责解析字符串并以有效的方式修改它们，而不必显式地遍历组成特定字符串的字符。我们还导入了自然处理工具包`ntlk`，这是最常用的 Python 库之一。它负责我们需要对文本执行的任何处理，以改变其形式或从中提取某些成分。类别建构函式会移除停用字词。这是一个相对较大的主题，您可以稍后阅读，因为它更多地涉及自然语言处理，而与我们的主题关系不大。

`processTweets`函数只是遍历输入其中的所有 tweet，在列表中的每个 tweet 上调用它的相邻函数`processTweet`。后者通过首先将所有文本转换成小写字母来进行实际的预处理。这仅仅是因为，在几乎所有的编程语言中，“car”与“cAr”的解释方式不同。因此，最好将所有数据中的所有字符都规范化为小写。其次，URL 和用户名从 tweet 中删除。这是出于我们在文章前面披露的原因。之后，数字符号(即#)从每个标签中移除，以避免标签被不同地处理。最后但并非最不重要的一点是，删除重复字符，以确保没有重要的单词未经处理，即使它以不寻常的方式拼写出来(例如，“caaaaar”变成了“car”)。最后，tweet 的文本被分解成单词(标记化)，以便在接下来的阶段中简化处理。

我们举个例子。数据集中可能会出现以下推文:

```
"@person1 retweeted @person2: Corn has got to be the most delllllicious crop in the world!!!! #corn #thoughts..."
```

我们的预处理器将使推文看起来像这样:

```
“AT_USER rt AT_USER corn has got to be the most delicious crop in the world corn thoughts”
```

最后，标记化将导致:

```
{“corn”, “most”, “delicious”, “crop”, “world”, “corn”, “thoughts”}
```

请注意，我们的代码删除了前面提到的单词中的重复字符(即“delllllicious”变成了“delicious”)。但是，它没有从文本中删除重复的单词(即“玉米”)，而是保留了它们。这是因为重复词在确定文本的极性中起作用(我们将在下一节中看到)。

我们已经准备好使用我们的预处理器类。首先，我们将创建一个引用它的变量(一个对象)，然后像前面讨论的那样在训练集和测试集上调用它:

现在我们可以进入最激动人心的部分——分类。但是首先，让我们重温一下我们的算法:朴素贝叶斯分类器。

# D 部分:朴素贝叶斯分类器

毫无疑问，计算机科学和机器学习中最重要的概念之一。直接进入 It 的数学领域可能会令人沮丧。因此，我不会从数学的角度来解释它。

> 成为计算机科学家不需要懂数学。然而，要成为一个真正优秀的人，你确实需要了解数学。

我想强调的事实是，我在这里只简要地解释朴素贝叶斯分类，因为深入的解释值得自己的长篇大论。

朴素贝叶斯分类器是一种基于贝叶斯定理的分类算法。该定理提供了一种计算称为后验概率的类型或概率的方法，其中事件 A 发生的概率依赖于概率已知背景(例如事件 B 证据)。比如，如果 Person_X 只在外面不下雨的时候打网球，那么，根据贝叶斯统计，Person_X 在不下雨的时候打网球的概率可以给出为:

```
P(X plays | no rain) = P(no rain | X plays)*P(x plays)/P(no rain)
```

遵循贝叶斯定理:

```
P(A|B) = P(B|A)*P(A)/P(B)
```

对于我们的任务，你只需要知道朴素贝叶斯分类器依赖于著名的贝叶斯定理。在我们继续之前，让我们快速概述一下接下来要采取的步骤:

> 1-建立驻留在我们的训练数据集中的所有单词的词汇表(单词列表)。
> 
> 2-将 tweet 内容与我们的词汇表进行逐字匹配。
> 
> 3-建立我们的单词特征向量。
> 
> 4-将我们的特征向量插入朴素贝叶斯分类器。

这可能看起来很多，但不要担心。它实际上非常简单，而且尽可能的短。让我们一步一步地把它记下来。

**步骤 D.1:构建词汇**

自然语言处理中的词汇表是模型可用的所有语音片段的列表。在我们的例子中，这包括我们拥有的训练集中的所有单词，因为模型可以相对平等地使用所有这些单词——在这一点上，至少可以这样说。代码看起来会像这样:

这只是创建一个我们在训练集中拥有的`all_words`列表，将它分解成单词特征。这些`word_features`基本上是不同单词的列表，每个单词都有其频率(在集合中出现的次数)作为`key`。

**步骤 D.2:根据我们的词汇表匹配推文**

这一步至关重要，因为我们将检查我们的训练集(即我们的`word_features`列表)中的所有单词，将每个单词与手头的推文进行比较，将一个数字与下面的单词相关联:

```
label 1 (true): if word in vocabulary is resident in tweet
label 0 (false): if word in vocabulary is not resident in tweet
```

这很容易编码:

给定最后一个代码片段，对于 word_features 中的每个单词，我们将拥有 JSON 键‘contains word X’，其中 X 是单词。根据我们之前所说的标签，其中的每个键都将具有值 True/False——True 表示“存在”, False 表示“不存在”。

**步骤 D.3:构建我们的特征向量**

现在让我们调用我们编写的最后两个函数。这将建立我们的最终特征向量，我们可以继续进行训练。

NTLK 内置函数`apply_features`从我们的列表中提取实际的特征。我们最终的特征向量是`trainingFeatures`。

**步骤 D.4:训练分类器**

我们终于完成了我们任务中最重要的——讽刺的是最短的——部分。多亏了 NLTK，我们只需要一个函数调用就可以将模型训练成朴素贝叶斯分类器，因为后者内置于库中:

我们快完成了！我们剩下的就是运行分类器训练代码(即`nltk.NaiveBayesClassifier.train()`)并测试它。请注意，执行这段代码可能需要几分钟时间。

# E 部分:测试模型

关键时刻到了。让我们根据我们的搜索词，通过对我们从 Twitter 下载的 100 条推文运行分类器(即`NBayesClassifier`)来完成我们的工作，并获得分类器返回的标签的多数投票，然后输出推文的总正面或负面百分比(即分数)。这也很简单:

就是这样！恭喜你。您已经创建了一个 Twitter 情绪分析 Python 程序。请注意，我们没有触及准确性(即评估模型)，因为这不是我们今天的主题。稍后我会在一篇文章中解释机器学习中的整个模型/假设评估过程。让我们最后看一下我们为此任务编写的完整代码:

# 结论

情感分析是一种有趣的方式，可以用来思考自然语言处理在对文本做出自动结论方面的适用性。它被用于社交媒体趋势分析，有时也用于营销目的。由于现代现成的库，用 Python 编写情感分析程序并不是一件困难的事情。这个程序简单地解释了这种应用程序是如何工作的。这只是出于学术目的，因为这里描述的程序绝不是生产级的。