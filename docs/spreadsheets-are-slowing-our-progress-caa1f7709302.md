# 电子表格减缓了我们的进度

> 原文：<https://towardsdatascience.com/spreadsheets-are-slowing-our-progress-caa1f7709302?source=collection_archive---------10----------------------->

## 当学术界关于可复制性危机的争论愈演愈烈的时候，还有一个更普遍的危机就在我们的眼皮底下

曾经有一段时间，我知道如何做分析的唯一方法是使用电子表格。我花了超过 15 年的时间在这些屏幕上建立高度复杂的模型和分析，这些屏幕上有很多人依赖的矩形盒子。

然后，2016 年初，我的一切都变了。对 R 和 Python 的大惊小怪开始了，我问了几个“了解内情”的人，他们认为哪种软件最适合进行最广泛的分析。我得到的一致回答都指向 R(大概是因为和我说过话的人)。所以我决定我要学习这个东西，看看所有的宣传是否值得。

六个月后，在经历了许多个深夜和周末后，通过寻找一切机会用 R 解决与工作相关的问题，我处于一种无法忍受再次在电子表格中工作的状态。我是认真的。今天打开它们是一件苦差事，我这样做的唯一原因是因为我和一些和我三年前处境相同的人交流。

我查看类似于`VLOOKUP`的函数，并将它们与`dplyr::left_join()`进行比较。这就好像我站在一条满是垃圾的街道上，一边是一个不幸的人，他有一个小垃圾收集器，正在一个接一个地收集垃圾，另一边是一个人拿着你见过的最大、最强大的垃圾吸尘器。

所以我认为电子表格对我们没有好处。他们把我们困在这一套狭窄的视图和选项中，在他们漂亮的外观和感觉上耗尽了我们所有的计算机内存，当有太多数据时，决定生闷气并冲进另一个房间，这一切都是因为(就像我们的孩子用 Snapchat 一样)我们已经沉迷于即时的视觉分析满足感。

多年来，电子表格造成危害还有另一个原因——它们造成了企业的可复制性危机。

# 什么是再现性危机？

科学方法的一个重要部分是要求重现结果以验证它们。大多数学者认为，至少在社会和生命科学领域，我们正处于可复制性危机之中。心理学是一个近年来被涂上厚厚一层油彩的领域。近年来,“研究”发表的速度导致了许多有问题的研究实践。在一项针对 2000 名心理学家的调查中，大多数人承认使用了至少一种有问题的研究方法，假阳性和确认偏差在受访者中普遍存在。当然，这种极端的结果是彻头彻尾的欺诈性研究，这是心理学和其他领域都无法避免的。

“流行心理学”出版物的兴起以及大众媒体对心理学理论和研究的大量引用导致了这样一种情况，即未经验证的想法正在作为“真理”获得地位，而没有人试图批评或验证产生这些理论的结果。在试图研究心理学中再现性危机的程度时，[研究发现](https://journals.sagepub.com/action/captchaChallenge?redirectUrl=https%3A%2F%2Fjournals.sagepub.com%2Fdoi%2Fabs%2F10.1177%2F1745691612460688)不到一半的验证先前研究的研究确实验证了它。

对于像心理学这样的领域，这可能是非常有害的。近年来，我们看到了一个积极的趋势，即越来越信任心理学家和心理计量学家在商业和企业中的价值，这是人们越来越认识到人才的战略重要性的一部分。但是，持续的无纪律出版无疑会在该领域造成越来越多的混乱和缺乏清晰度——很可能会有一天，你可以找到一些东西来支持你想表达的任何观点。从长远来看，这种稀释会损害油田。

![](img/b8cf9d11bb88969b4acf4606f510ea40.png)

# 电子表格和这有什么关系？

暂时把学术放在一边，我认为在企业或公司环境中，分析需要可复制才能成功。通常不一定要验证以前的结果(尽管我认为这总是一件好事)，但出于操作原因，通常需要重复类似的分析。我们看到，在企业环境中进行的分析的性质和类型越来越复杂，进行一次这样的分析而没有简单的方法在未来复制它是非常危险的。当环境发生变化时，可能需要再次运行分析，或者企业中的另一个团队可能需要为了不同的目的而尝试重复分析，

电子表格使得重现分析变得非常非常困难，特别是如果它本质上是复杂的。以下是几个原因:

1.  电子表格的结构是混乱和非线性的。要追踪一个特定的值，您必须找到位于原始分析师选择的位置的从属值。你最终会在 EE:1254 单元格中某个名为“不重要”的隐藏表中找到它们。什么？
2.  电子表格使得评论变得困难。当它跨越多个工作表和单元格时，作者很难解释他们在做什么。
3.  电子表格将用户限制在一个共同的、狭窄的操作环境中。这使得非电子表格用户很难轻松直观地挖掘和理解已经完成的工作。相信我，非电子表格用户正在增加。

开源数据科学语言克服了所有这些挑战。每个人都可以访问他们需要的软件和代码库。代码是以线性的、逻辑的方式编写的，注释也很容易，因此其他用户可以理解你的逻辑，并准确理解你在每一步做什么。通过 Markdown 和 Jupyter 笔记本将代码集成到垂直文档中的能力使我们能够编写包含方法、代码和结果的完整研究描述。

# 对此我们应该做些什么？

如果你是一家企业的分析主管，而这家企业的大部分工作仍然是使用电子表格完成的，那么你就真的陷入了企业可复制性危机。是时候咬紧牙关向编码语言迈进了。这并不容易，开始可能会很艰难，但有了正确的承诺和资源，这是非常可行的。

如果你已经踏上了这条旅程，这里有一些我坚持认为有助于工作重现性的最佳实践:

*   将鼓励和激励放在适当的位置，以确保所有代码都被自由地评论
*   确保所有新的研究都写在一个包含嵌入式代码的垂直文档中(比如 R Markdown 或 Jupyter Notebook)。
*   如果需要从以前的电子表格方法中复制一项工作，不要费心试图将电子表格拆开，只需从头开始，再次定义需求，并在新的环境中从头构建它。拆开一份电子表格就像让那个拿着垃圾收集器的人把他所有的东西放回原位，然后我们再用那个强大的真空吸尘器把它们全部吸走。这是毫无意义的，徒劳的努力。

我们可以轻松复制分析的未来是一个令人兴奋的未来，实现这个未来也越来越重要。但电子表格不会帮助我们实现这一目标。

最初我是一名纯粹的数学家，后来我成为了一名心理计量学家和数据科学家。我热衷于将所有这些学科的严谨性应用到复杂的人的问题上。我也是一个编码极客和日本 RPG 的超级粉丝。在 [*LinkedIn*](https://www.linkedin.com/in/keith-mcnulty/) *或*[*Twitter*](https://twitter.com/dr_keithmcnulty)*上找我。*