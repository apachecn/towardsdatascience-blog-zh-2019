# 关于我如何认识基于人的偏见以及如何处理它

> 原文：<https://towardsdatascience.com/on-how-i-acknowledge-human-based-bias-and-how-to-handle-it-933479a623fa?source=collection_archive---------21----------------------->

## 关于我们，数据从业者，应该如何更加意识到和关注我们自己的偏见

在数据科学的世界中，我们将**偏差**定义为系统从其数据中过度概括并学习错误内容的现象。当这种情况发生时，我们通常采取的第一个行动是指责数据或训练过程，然后说*“这个数据不好”*或*“我应该进一步调整我的超参数。”当然，这可能是问题的一部分。然而，在花费更多的时间和处理能力之前，我想请你停下来，后退一步，想想我们正在使用的数据是如何来的，更重要的是，让我们思考一下我们是如何解释它的。*

与机器和聪明的学习者不同，我们人类会受到偏见的困扰，这种偏见可能是由多种原因引起的，比如我们以前经历过的时刻，或者已经成为我们一部分的概念和定义。不幸的是，这种偏见可能会影响我们处理和解释数据的方式，当我们不经意地将这些想法和假设转移到我们的数据集，从而转移到我们的机器学习模型及其结果时，就会产生问题。这些后果的例子经常在媒体上被提及(通常带有令人不快的散布恐慌的标题)，例如亚马逊著名的“性别歧视”招聘模式，该模式优先考虑男性候选人而非女性候选人。

在这篇文章中，我讨论了偏倚的三个来源，确认偏倚、可用性启发式和样本偏倚，并写了我是如何认识到它们的存在和影响的，以及我用来处理它们的几种技术。

![](img/ba5e29d7f5548fbd64d232502fa7fcec.png)

自 2016 年以来，我一直在一个约会和社交平台的反垃圾邮件团队工作，我的目标是建立检测垃圾邮件发送者的解决方案，并避免它们的扩散。在我开始在公司的职业生涯时，我对我们的用户一无所知(如我所料)；我并不完全了解我们的人口统计数据，也不了解他们的行为模式。我想说的是，从简单的一瞥中，我无法判断一个用户是否是垃圾邮件发送者；任何人都可能成为其中一员！然后，随着每一天的过去，你开始体验和学习事物。*啊，这个地理区域好像更垃圾啊，啊，这个邮箱域是可怕的新闻啊，这样的名字从来都不好，*等等。简而言之，我纯粹基于我所学到的、看到的和处理过的，创建了一个垃圾邮件发送者的心理轮廓。现在我不得不问自己:这种知识是公平的吗？这个侧写能代表全部人口吗？我心目中的“理想”垃圾邮件发送者形象是公正的吗？这些是我每次处理数据时都会问自己的一些问题，最重要的是，每次我训练一个新的机器学习模型时都会问自己。我为什么要问这些问题？嗯，首先，我认为在这一行你应该经常质疑自己。第二，因为这就是我承认**基于人类的偏见**的方式，以及如果我忽视它可能产生的影响。

在所有现存的偏见中，有三个主要的——T4 确认偏见、**可用性偏见**和**选择偏见**——我认为如果我不考虑它们，可能会在我的模型中造成不必要的影响；这并不意味着我不介意其他偏见，只是这些偏见让我保持警觉。在接下来的几行中，我将定义这些偏见，并给出一些它们如何影响我的例子。

确认偏差是[认知偏差](https://en.wikipedia.org/wiki/Cognitive_bias)的一种，指的是以支持和确认一个人的观点和假设的方式解释信息、证据和数据的倾向，同时忽略任何可能的冲突证据。确认偏见是最常见的偏见之一，不难想象为什么会出现这种情况，毕竟，根据我们支持的东西来支持和确认想法，在某种程度上，就像是合乎逻辑的事情。前面，我提到了一些可能的理论和特征，这些理论和特征是我与垃圾邮件发送者一起工作了这么长时间后了解到的，例如，如果某个用户位于某个特定区域，那么他就是垃圾邮件发送者的可能性。这个事实似是而非。有些地区的垃圾邮件发送者比其他地区更集中，因为这种模式在某种程度上很常见，我可能会“无意识地”了解并确认如果用户 X 来自地区 Y，他可能是垃圾邮件发送者。但是，这是否足以证明这个用户是真正的垃圾邮件发送者呢？当然不是！尽管如此，在特定和不利的情况下，例如，如果我必须在压力大的一天标记用户配置文件，我可能会意外地将该用户标记为可疑用户，从而证实我的偏见，因为我的假设表明该用户可能确实是垃圾邮件发送者。尽管如此，我很少手动这样做，所以这种情况发生的几率几乎为零。

可用性启发，另一种认知偏差，描述了每当遇到决策情况时，人们倾向于重视最近和最直接的经验、信息或想到的例子。这种思维捷径背后的主要思想是，如果一个人记得一条信息，那就意味着这条信息是必不可少的。在处理数据和决策系统时，忽视这一假设的存在会导致灾难性的结果。原因如下。

通常，在我的工作时间，同事们会过来问我某个档案是不是垃圾邮件。通常，我会马上回答，因为我很熟悉垃圾邮件发送者的样子(我听起来有偏见吗？).话虽如此，我必须承认，在有些情况下，我不愿意不假思索地快速回答是或否。这是为什么？因为我确定我见过这样的案例。例如，我每天都会看到许多个人资料和他们的用户名，我已经熟悉了许多模式和关键字，这些模式和关键字表明所述用户名是否与垃圾邮件个人资料相关。所以，如果你随机问我，什么是典型的垃圾用户名，我可能会有答案。

另一个例子是标注数据时。尽管这个过程是自动的，但我还是时不时地深入数据集，寻找异常值或需要人眼观察的奇怪案例。在这些行和特征的海洋中探险的过程中，我可能会看到一个特殊的例子，在这个例子中，我的大脑通过可用性启发法，根据最近的经验，可能会确定某个配置文件是垃圾的还是好的。在这种情况下，最简单的解决办法就是听听我大脑中的声音，然后改变标签(老实说，如果我有 100%的把握，我会这么做)，然而，因为我意识到了这种偏见，我会首先咨询我们的其他来源来确认或否认我的信念。

最后，还有样本偏差，一种统计偏差。当为训练您的系统而选择的数据不代表将使用该模型的总体时，会观察到这种偏差。结果很可能是一个有偏差的样本，一个过度代表一个群体而不足代表其他群体的数据集。消除这种偏见并不是一件容易的事情，在实践中很可能会发生，因为正如维基百科所说的那样，在采样中“[几乎不可能确保完全的随机性](https://en.wikipedia.org/wiki/Sampling_bias#Problems_due_to_sampling_bias)，”然而，意识到它的存在可能有助于减轻它的影响。这种偏见可能会以无数种方式出现在我的日常生活中，在下一段中，我将举例说明我发现的一些方式。

首先，我总是在考虑时区。这是因为每当我做一些与时间相关的事情时，例如，从过去的 Y 个小时中选择 X 个数据，我的样本将主要由在这 Y 个小时中处于高峰期的地理区域的观测数据组成。例如，我在欧洲，所以如果我在上午 9 点查询选择前一个小时的 X 件事，我的样本很可能是欧洲用户和失眠的人。因此，在某种程度上，我给我的采样数据增加了偏差。我发现的另一个例子是平台和应用程序版本之间的差异。在查询数据时，我们必须记住，用户正在使用不同的平台或应用程序的发布版本，这意味着他们可能会生成不同类型的数据。例如，假设有一天一个产品团队决定在应用程序的下一个版本中，用户将被允许上传一百万张图片到他们的个人资料中。然后，在同一天，一个随机的非常不幸的机会，我决定建立一个模型，根据图片的数量来检测垃圾邮件发送者，而不知道应用程序中的这种变化。然后，由于“百万图像”功能是新的，并不是每个人都会有更新，我不会很好地代表这个在他们的个人资料上有百万图像的新群体，这将在训练和推理时间产生一些不想要的结果。

## 解决方案？

有没有办法完全避免基于人类的偏见？我不知道，但我确信，作为从业者，我们可以采取一些措施来减轻它们对我们数据集的影响，从而减轻我们决策模型的影响。

我的第一个建议是数据驱动。我指的不是数据驱动的含义*“哦，是的，我在做决定之前阅读我的数据”*并进行一些查询。我的意思是**挤**，**合二为一**，**钻研**，见鬼，**爱**那些数据集。画出它们的分布，去除离群值，对它们进行聚类，测试它们，降低它们的维数等等。确保你真正了解他们。

与前一个技巧密切相关的另一个技巧是识别偏差的可能来源。在一张纸上、维基页面、便利贴或手背上写下可能给你的系统带来偏见的内容。是时间，还是应用程序版本的差异，就像我提到的那样？像我一样质疑自己。问问自己，你的样本数据是否能代表总体，或者你将要做出的决定是基于真实的信息，还是基于你对昨天数据点的直觉。

最后，与他人分享你的过程。与你旁边的人交谈，询问他们对你的代码或查询有什么看法，或者创建一个拉请求，以便其他人可以仔细检查你的工作。有时候，因为我们离材料如此之近，如此执着于材料，我们看不到别人能发现的错误和细节。

## 结论

我们人类是有偏见的。如果这种基于人类的偏见没有得到正确处理，它可能会影响我们工作和解释数据的方式，最终会影响结果——在大多数情况下，这是一种不可取的结果——以及我们的机器学习模型的性能。在本文中，我介绍了三种偏差:确认偏差、可用性启发和样本偏差，并谈到了它们在我日常工作中的许多表现方式，并提供了一些如何减轻其影响的建议。

忽视这些偏见的存在可能会在我们的系统中导致不必要的和灾难性的行为，在大多数情况下，这些反应会让我们产生*“嘿？为什么我的模型认为这是一只猴子？”*——诸如此类的问题，导致耸人听闻和散布恐慌的文章，声称艾是种族主义者、性别歧视者、精英主义者或者仅仅是明显的不公正。我真诚地相信，每个与数据打交道的人都应该意识到这可能对他们的工作产生的影响。随着机器学习在我们生活的各个方面的快速采用，我们的产品可能会变成一个有偏见的系统，不幸的是，它可能会导致致命的事故，诊断出不正确的治疗方法或阻止你的整个用户群。