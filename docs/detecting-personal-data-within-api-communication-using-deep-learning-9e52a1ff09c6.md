# 使用深度学习检测 API 通信中的个人数据

> 原文：<https://towardsdatascience.com/detecting-personal-data-within-api-communication-using-deep-learning-9e52a1ff09c6?source=collection_archive---------6----------------------->

![](img/d955f6656c81773749ce367e321e901c.png)

# 概观

有没有想过有多少个人数据分散在各个组织中？大量的个人数据——你的、我的、每个人的——从模糊的个人信息到极其具体的信息，都在四处漂浮。大多数情况下，它是未被发现的。几乎总是，它被你给它的组织使用，有很好的理由。有时，出于可疑的原因。经常(非常，非常经常)它被第三方出售和使用，或者被误用。).太多时候，个人数据被劫持并用于邪恶的目的。鉴于在线个人数据的使用和滥用机会呈指数增长，难怪欧盟最近通过了《通用数据保护条例》(GDPR)，该条例于 2018 年 5 月 25 日生效。一个月后，加州紧随其后，颁布了《加州消费者隐私法》(CCPA)。如果你想知道有多少组织掌握着你的个人数据，你并不孤单。但是那些组织本身呢？监控这些数据既困难又耗时。这种个人数据噩梦最可怕的部分可能是，组织本身往往不知道你的个人数据存储在哪里，它可能流经哪些应用程序，或者它可能最终会在哪里。监管个人数据的流动和使用的趋势正在上升，但你如何监管你无法检测到的东西？

GDPR 法规的支柱之一是，任何处理个人数据的应用程序都应该“嵌入”隐私，通常称为隐私设计(PbD)。这远不是一个新的定义:

> “隐私设计方法的特点是采取主动措施，而不是被动措施。它可以在隐私侵犯事件发生之前预测并阻止它们。PbD 不会等待隐私风险的出现，也不会在隐私侵害发生后提供补救措施来解决隐私侵害——它旨在防止隐私侵害的发生。简而言之，隐私是事先设计好的，而不是事后的”
> 
> A.卡沃金。设计隐私——7 项基本原则，2011 年 1 月。

这遵循了类似于安全设计的原则(不幸的是，我认为我们离安全设计还很远)。隐私和安全的设计听起来都很棒。但是，如何处理已经发布并投入生产、传输和接收个人数据的数十亿行代码呢？我们是否要等待数据泄露发生，然后应用修复程序？对我来说，这听起来太少，太晚了。

为了寻找灵感，我开始研究一个相关领域:网络安全。我了解得越多，就越发现个人数据共享和网络安全问题之间的相似之处。在必须应对应用程序和基础架构中的新旧未知威胁方面，挑战是相似的。一种常见的缓解机制是持续监控网络流量，检测可能转化为实质性威胁的潜在恶意模式。

我认为，涉及个人数据处理的威胁与网络安全威胁一样重要。在这两种情况下，它都归结为暴露，这总是以这样或那样的方式转化为财务损失，影响负责处理个人数据记录的组织。这反过来影响他们如何处理这些个人记录；这对我们所有人都有影响，有时影响非常大。

但是说够了，是时候动手了。

# 训练数据集生成

为了通过深度学习获得相当不错的结果，训练需要大量的正面和负面例子。这些例子越真实，预测就越准确。

我面临的第一个挑战是如何获得如此庞大的样本集，因为根据定义，个人数据是保密的，因此不会公开。

有许多方法可以获得这种数据来检测应用程序安全异常，例如利用动态应用程序安全测试(DAST)工具，该工具包括生成和捕获恶意流量，然后基于此训练分析模型。然而，在我们的案例中，包含个人数据流的流量并不意味着安全威胁，因此 DAST 工具或它们通常生成的流量数据不提供覆盖范围。

第二个挑战？除了包含虚构的个人数据之外，我还需要对个人数据在 API 通信(例如 REST)中通常是如何传递的进行编码，因为这是我们将要运行预测的对象。例如，个人数据属性通常只代表整个 REST API 有效负载的一个子集。

最后，我还需要网络来了解个人数据和有效载荷的规律。简而言之，它不仅要学习不同形式的个人记录，更重要的是，还要学习通过网络交换的个人数据是什么样的。

我应对这些挑战的方法是使用模式作为主要来源，精心制作我自己的机器生成数据集，也称为合成数据集。

好消息是大多数流行的 REST APIs 都附带了一个 OpenAPI(以前称为 Swagger)描述符。

> OpenAPI 规范，最初被称为 **Swagger 规范**，是用于描述、产生、消费和可视化 RESTful web 服务的机器可读接口文件的规范。

因此，给定一个 OpenAPI 描述符，我只需基于这个蓝图实例化一个 RESTful 请求，在给定数据类型的情况下，用虚构但格式良好的值填充空白。最新的 OpenAPI 描述符目录可在 https://github.com/APIs-guru/openapi-directory 获得。数据集生成器扫描该目录，并基于该目录实例化合成请求有效载荷的集合，该集合随后用于训练网络。

下面是综合请求生成器的核心部分:

REST APIs 的局限性之一是尽可能避免传递个人信息。取而代之的是，使用一个或多个不太敏感的标识符，以便服务可以解析到相应的 PII，而无需公开完整的记录。这是在有两个少数正面例子(即包含 PII)导致高度不平衡的数据集的情况下得出的。我采取的缓解此问题的方法(见第 21-30 行)是通过使用最近的正面示例(PII 请求有效负载)作为模板进行过采样，以生成包含一些其他随机选择的 PII 属性(如 SSN、电话号码等)的其他正面示例。).

该项目捆绑了一个预生成的训练数据集，位于 *data/training.csv* 下。

以下是我们的“假”有效载荷的摘录:

现在，让我们获取我们生成的数据集的一些指标:

> 0 19278
> 1 22607
> 数据集中包含 PII 的请求:53.97%

我们已经能够生成足够大且平衡的训练数据集。

不错吧？让我们使用它。

# 选择 DNN 发动机

正如您可能已经知道的，有几个很棒的 DNN 堆栈，支持多种网络拓扑结构。我们将选择 TensorFlow，它最近受到了很多关注，因为到目前为止，该领域的大多数研究都是在这里进行的。

为了保持人工智能相关的复杂性，以及能够快速迭代，我们将抽象特定的堆栈(TensorFlow)并使用 Keras，Keras 将负责设置网络层所需的繁重工作。

因为我们的 DNN 堆栈是用 Python 实现的，所以我们的解决方案需要使用相同的语言来实现，以实现无缝的互操作性。

# 了解“个人”的含义

我们应该使用哪种可用的神经网络拓扑结构？

很明显，我们在按照一套既定的规则处理信息。例如，一个有效的 JSON 文档遵循特定的约定——在其语法中指定——这是我们需要考虑的。这方面的一个例子是数据由逗号分隔，花括号包含对象，等等。

此外，值可以遵循各种各样的格式，其中许多是位置相关的。例如，社会安全号码不同于电话号码。让网络学会在这一水平上进一步辨别将提高预测的准确性。继续前面的例子，如果属性名是“ssn ”,但是对应的值与学习到的 SSN 格式不匹配，那么它的得分将低于遇到格式良好的 SSN 值时的得分。

总之，我们必须学习序列，包括 JSON 文档的术语和其中定义的值的字符模式。到目前为止，这种情景的最佳匹配是 LSTM(长短期记忆)。这种类型的 RNN(递归神经网络)带来的主要特征是状态性。简而言之，在处理输入时，它会考虑之前看到的内容。它有记忆。例如，如果它看到下面的 JSON 键/值对:

> { " SSN ":" 744–22–5837 " }

在学习值部分的序列(即“744–22–5837”)时，它将考虑之前看到的密钥(即“ssn”)，从而在提取其处理的令牌背后的正确含义方面增加了更多信心。

这里是实现位。LSTM 隐藏层输入单词 embedding——很像一个从有效载荷中提取文本的字典——并有单独的丢弃层以减少过度拟合；和最后的输出层，以产生 PII 分类。我们将使用 100 个历元，因为这是模型与我们的合成数据集聚合的地方。我强烈建议使用体面的 GPU，以便通过这一点明显更快。

现在是训练神经网络的时候了。默认情况下，它将使用项目附带的数据集(training.csv)。

> $ python privapi/train.py

超过 **99%** 的准确率！到目前为止，一切似乎都很有希望。接下来呢。现实检查。

# 检测个人数据

我们训练好的网络模型现在可以预测一个给定的 JSON 有效载荷中是否有 PII。

我们的分类器将遍历包含示例请求有效负载的文件夹，并将使用先前生成的神经网络模型获得的预测输出到 CSV 文件中:

在“预测”文件夹中，我们有两个要对其运行预测的示例。

注册 webhook 的示例**非敏感** [Slack](http://slack.com) API 有效负载:

和一个**敏感的**请求有效载荷——因此包含 PII——用于 [Magento](http://magento.com) 电子商务解决方案:

让我们运行预测器:

> $ python privapi/predict.py

该命令将遍历包含示例请求有效负载的文件夹，并将预测输出到名为 *predictions.csv* 的 CSV 文件中，如下所示:

这表明，至少在这两个例子中，我们的预测器做得非常好。

首先，它检测到 Magento 有效载荷确实很敏感，得分几乎是 100%。其次，它将松弛有效载荷归类为不敏感，准确率约为 40%。

有趣的是，这个有效载荷包含了可能被错误地认为是 PII 的内容(例如，名字和姓氏)，但是它并没有强烈地影响分类，以至于选择了错误的类。

我建议您尝试使用您喜欢的请求有效负载，看看您会得到什么结果。

# 带回家的体验

老实说，我对当前最先进的人工智能如何在隐私领域做出贡献印象深刻，主要是通过让处理和传输我们个人数据的组织产生意识。我相信机器有很多机会来学习如何帮助保护我们的个人数据安全。我将这个项目命名为 PrivAPI，并在 Github 上公开。请随意查看、体验，并做出贡献。

# 我们将何去何从

PrivAPI 还有很大的改进空间。主要领域包括:

*   **流式传输:**从事件流式传输平台获取 REST API 有效负载，并将神经网络模型应用于新事件，以推断结果(即有效负载是否保密)。最后，将预测推给任意的消费者，让他们据此采取行动。
*   **在线学习:**不要将训练和推理分开，而是允许从接收到的 REST API 有效负载中进行训练，这样解决方案的整体有效性就会得到提高，因为它正在学习特定组织内的 API 流量模式。
*   **神经网络监控和警报:**监控神经网络模型的准确性、分数、SLA 和其他指标，并实时提供自动警报。最后，反馈度量以改进或替换神经网络模型。
*   **额外的有效载荷格式:**处理使用另一种符号表示的 API 流量应该非常简单，因为神经网络与此无关。例如，支持 XML API 有效负载将允许我们监控 SOAP 流量，这在企业环境中仍然非常普遍。

你想在 PrivAPI 中看到什么？欢迎在下面发表评论，贡献一个 Github pull 请求。

查看 GitHub 上的代码:

[](https://github.com/veridax/privapi) [## Veridax/privapi

### 使用深度神经网络检测敏感的 REST API 通信- Veridax/privapi

github.com](https://github.com/veridax/privapi)