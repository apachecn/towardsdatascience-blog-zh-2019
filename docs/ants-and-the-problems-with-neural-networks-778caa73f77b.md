# 蚂蚁和神经网络的问题

> 原文：<https://towardsdatascience.com/ants-and-the-problems-with-neural-networks-778caa73f77b?source=collection_archive---------7----------------------->

## ***认知科学可能如何改变神经科学***

![](img/266137d1ec31c1de610b6d5929a38f4f.png)

Photo by [Mikhail Vasilyev](https://unsplash.com/@miklevasilyev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一个nt 是相当愚蠢的。它们能活一周，除了四处走动、寻找食物和为它们的蚁丘搬运小树枝之外，不做太多事情(现在我想起来，我们人类也不做太多其他事情)。

但是，除了过着平淡无奇的蚂蚁生活之外，他们也是愚蠢的。从技术角度来说，它们是愚蠢的:一只蚂蚁只有大约 250，000 (2,5*10⁵)个神经元。作为比较:一个普通的智人平均有 800 亿个神经元(8*10 ⁰)，所以如果我们假设智力至少在某些方面与大脑的大小成比例(忽略一些动物的大脑比我们大的事实)，那么我们大约是蚂蚁的 320，000 倍。

尽管蚂蚁的大脑很小，但它们也有自己的时刻。他们不断地做一些非常复杂的事情，以至于可以直接通过大学水平的数学考试。其中一个东西叫做 ***航位推算*** 。

## 航位推算

当像 ***双色斑翅蚁*** 这样的蚂蚁外出觅食时，它们会离开家，朝着预期食物来源的方向移动。由于他们不知道食物来源的确切位置，他们走在摇摆不定的路线和圆圈中(更多细节和图解见 Maroudas 和 Harkness 的论文)。如果你在野外观察过蚂蚁，你可能会认为这一切看起来完全是随机的。

但是一旦蚂蚁找到了食物来源并得到了它的那份食物，它就会直接回到它的家。而我说的直线，我指的是字面上沿着 ***的直线，不借助任何地标*** 来指引它们。

***航位推算*** 是一种通过回忆自己从哪里来，从而知道自己在哪里的艺术。没有人真正知道为什么它被称为航位推算。你需要非常活跃才能做到。这不是一个简单的任务。

对于蚂蚁来说，要想知道它们在哪里，它们需要考虑它们在某个方向上行进的时间和速度。他们需要对长时间内路径上的所有微小位移进行汇总，并且他们需要能够随着时间的推移可靠且可访问地存储这些信息。

在数学中，你称这个过程为 ***路径积分*** ，因为你在一段时间内对微小的位移进行积分，得到一个总和，然后你可以用它来计算有用的东西。

然后蚂蚁需要利用这些信息来计算出回家的最佳路线。为了做到这一点，蚂蚁必须 ***隐含地理解直角三角形的样子。*** 知道了它总共走过的路径的总位移(比方说，向北 10 米，向东 5 米)，如果它想回到最优路径，它需要在直角三角形 的**斜边上行进。**

要沿着斜边行进，它需要找到合适的角度，这个角度就是**北和**东位移比例的**反正切**。

我们并不知道蚂蚁是如何做到这一点的。

但是如果我们试图建造一个完成这项工作的设备，我们会假设我们需要以一种可靠的方式建造它，关于蚂蚁位置的信息以一种可靠的方式存储，并且在需要的时候也可以通过 ***计算访问*** 因为它需要它来计算蚂蚁在返回的路上将要采取的路线的角度，并且它需要能够独立于它去了哪里和它花了多少时间寻找食物来完成这项工作。

这一点在 A. King 和 C.R. Gallistel 的《改变思维的 ***记忆和计算大脑:为什么认知科学会改变神经科学*** 》中反复提到(我偷偷为我的标题修改了副标题)。

这篇文章是这本书的一些重要方面的 TL:DR 版本。这本书用了大得多的篇幅来阐述类似的观点。如果为了简洁起见，我不得不牺牲一些细节，我很抱歉，但我相信这些见解是高度相关的，并希望以一种不太耗时的格式来浓缩它们。

现在，记住 ***航位推算*** 是蚂蚁日常做的事情，也是过蚂蚁生活所需的许多其他任务之一。记住他们只有 25 万个神经元。

蚂蚁的大脑不是我们建造的，而是经过数百万年的进化而形成的。神经科学家面临的问题是，蚂蚁的大脑是如何连接的，以便以最佳方式进行这类计算。大自然已经一次又一次地证明了它在花费资源方面的吝啬，所以它很可能会认为它使用了一种为这项任务而优化的架构，尤其是考虑到蚂蚁大脑的大小。

作为一个物理过程，大脑必须遵守物理规则和计算的基本规则(由图灵等人制定)，就像任何其他计算设备必须遵守的一样。尽管大脑确实“与普通计算机的工作方式非常不同”，进行“大量的并行处理”，并拥有“大量的神经元连接”，但大脑的这些特性不应该成为重新描述大脑本身某种神奇能力的借口。

所以我们可以继续提问:基于神经网络的神经元架构能在多大程度上完成这类任务？

## 神经网络的问题

> “先说实话:机器不会学习”
> —安德烈·布尔科夫在长达百页的机器学习书中

![](img/ac89ac2b2b2978c3906e9899c0535fae.png)

Photo by [Franck V.](https://unsplash.com/@franckinjapan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

机器学习(ML)为我们提供了极其强大的分类学习算法。这是一种从数据中推断模式和结构的艺术，而无需给出如何推断这些模式的明确指示。

ML 方法让我们做了很多疯狂而有用的事情。如果目前围绕神经网络的大肆宣传是可信的，那么看起来它们可以学会做任何事情。我们需要注意，神经网络不会在未来几年失去控制，迎来由人工超级智能主导的人类反乌托邦未来。

但是根据安德烈·布尔科夫的说法，机器实际上“学习”的意义与我们或动物学习的意义相同，这有点牵强。对于通常的监督学习过程，我们只是进行大量的参数调整:我们试图找到由以下等式给出的决策边界(所谓的*、*、**、、**中的超平面，它们只是二维空间中的一条线)

**wx** -b=0，

为训练数据提供良好的分类结果。

当机器“学习”时，权重 **w** 被调整，以便在特征空间中找到决策边界，该边界为任何任意特征向量 **x** 给出最佳分类结果。

为了更加复杂，我们可以使用*核方法*来使特征空间中的度量在样本环境中非线性缩放，或者我们可以使用*支持向量机*来映射到具有其他维度的特征空间，我们可以调整神经元的*激活函数*等。

但这并没有改变机器学习算法的一个基本事实: ***在神经网络中并没有进行实际的计算。***

从这个意义上说，神经网络只不过是复杂的 ***查找表*** (在计算机科学中，它被称为计算设备的*有限状态架构*，类似于图灵机，但没有读/写存储器):它们预先指定特定输入的特定输出。他们如何进行这种映射对用户是隐藏的(特别是当使用字面上称为 ***隐藏层*** 的东西时)，并且关于网络如何分类的信息通常被编码在结构中并通过整个网络传播。

因此，它们的功能是 ***不具有代表性:*** 输入的任何表示都不会通过网络传送，并且可以通过网络中的每一步进行追踪。输入和输出就是一切。没有中间步骤， ***网络不需要知道输入是什么意思就可以处理。***

## 神经网络和联想学习

> “所有的模型都是错的，但有些是有用的。”
> —乔治·博克斯

虽然神经网络在某种程度上受到了大脑运作方式的启发，但神经科学家不一定认为神经网络足以代表大脑的工作方式。许多生物学的复杂性都被丢弃了，神经元通常以一种极其简化的方式来表示([树突的作用](https://neurophysics.ucsd.edu/courses/physics_171/annurev.neuro.28.061604.135703.pdf)或突触处的钙流，以及许多其他东西，在模型中都被忽略或大大简化了)。

然而，神经网络目前的成功与心理学中可能最突出的学习理论不谋而合:即 ***联想学习*** 。信息是通过加强或削弱大脑不同神经元之间的连接来处理和整合的，遵循的规则是著名的流行语:“ ***【什么东西把电线连在一起】*** ”。

***突触连接*** 是大脑在学习过程中调整的参数，因此它们的功能类似于人工神经网络中的权重。

就我自己而言，这让我相信神经网络真的可以在原则上解决他们面临的几乎所有任务，因此，大脑具有与人工神经网络非常相似的架构和学习机制。

***但这种观点存在一些内在问题。***

一个问题是，人工神经网络中最流行的学习方法(如*和 ***【梯度下降】*** )作为生物系统实际使用的方法是不现实的，因为它们需要用权重值进行计算，这又意味着网络外部的*无所不知，可以访问权重值并相应地改变它们。**

**但是突触权重是生物系统无法通过计算获得的。它们在人工神经网络中，但只是因为这些变量的值也存储在计算机的其他地方，而计算机本身不是神经网络。这反过来意味着神经元的功能结构对大脑本身来说是不透明的，它不能用来以一种允许大脑在需要时使用它的形式存储信息。**

**关于大脑是否使用*符号表示它正在处理的事物，在神经科学界有一个持续的争议，就像基于图灵机概念的计算设备一样(我在这里详细介绍了图灵机的基础知识[，](https://medium.com/@haxelschnurtz/a-non-technical-guide-to-turing-machines-f8c6da9596e5)，并解释了记忆和符号的功能)。***

***也就是说，这意味着一个读/写头可以访问它正在计算的符号，以及一种对计算进行编码的符号语言。正如我前面所描述的，神经网络是 ***而不是代表*** ，它们不处理输入的符号表示。***

**这一点把我们带回到蚂蚁身上，以及它们是如何在觅食后返回它们的山丘的。**

## **又是蚂蚁**

**![](img/f954728d71f7948faf2b79ae559708e6.png)**

**Photo by [Thomas Kinto](https://unsplash.com/@thomaskinto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

**正如我们所看到的，对于一只成功导航回蚁丘的蚂蚁来说，它看起来很像是有一些方法来将其当前位置存储在变量 中，并使用该当前位置变量来计算返回的最佳路线。**

**King's 和 Gallistel 指出，对于由神经网络解决的*航位推算任务，网络的计算和物理需求将*。****

***这是因为网络不擅长记忆，即动态存储信息。在为学习程序优化后，它在运行时基本保持不变。这就是布尔科夫所说的网络不会学习的意思，因为它们只在学习任务时发挥灵活性，而不是在执行任务时。***

## ******作为记忆的循环反馈回路******

***鉴于这个问题，已经进行了一些尝试来在网络中建立能够动态存储信息的体系结构。它们基于所谓的 ***循环反馈回路，可以作为网络的记忆。******

**在这里，记忆这个术语再次在图灵的广义上使用: ***作为一种可靠地携带计算所需信息的手段*** 。**

**循环反馈回路是神经网络中自我维持活动的突起。这种持续的活动可以起到符号的作用，因为活动 ***的信号需要时间来传播*** ，因此将它编码的符号 ***在时间*** 上向前传送。由于权重在神经网络中是不可计算的，所以符号必须被动态编码，因此存储器将动态操作。**

**这种方法在早期的模拟计算机中使用，但当新的发展提供了更好的存储信息的方法时，这种方法很快就被放弃了。**

**在神经网络中实现该技术的一种方法是使用 ***连接到权重为 1*** 的自身的循环神经元，因此它们通过一次又一次地激活自身来存储信息。**

**例如，在航位推算模型中，神经网络中活动高峰的位置可以对蚂蚁的位置进行编码。网络中相应位置的神经元会继续自我激活，直到蚂蚁继续前进。**

## **问题**

**当一个人试图在实践中实现这个想法时，事情变得复杂了(详见 Samsonovitch 和 McNaughton 的论文)。**

**这里不涉及太多的细节，作为记忆的循环反馈回路有几个固有的问题，特别是当它涉及到长期记忆时:**

1.  **大脑在花费资源方面极其吝啬。任何一个头脑正常的计算机工程师都不会想到建造一个通过自持电流来存储信息的硬盘。摩擦和连续加热会导致 ***能量消耗*** ，这是不必要的，也是不合理的。想象一下，为了不丢失其中的所有信息，你必须插上硬盘/u 盘并不断冷却它。**
2.  *****自然是凌乱的*** 。动力系统容易受到扰动，由于大多数动力系统的非线性，小扰动往往会随着时间的推移而放大(并非所有东西都是谐振子，因为本科物理学家往往会在花两年时间研究它后发现很多令人懊恼的事情)。如果您通过值为 1.01 的砝码发送值为 1 的信号，而不是通过值为 0.99 的砝码发送值为 1 的信号，那么在运行 50 次后，信号强度将为 1.64，而不是 0.61。当人们想到真实神经元的物理现实，及其所有的子结构、对神经递质的依赖性、钙流等时，对这种小扰动的定位一点也不牵强。假设它会将特定信号长时间保持在恒定的循环中，这可能是一种不切实际的简化。更有可能的假设是，自然界选择储存信息的实际机制以不同的方式工作，以一种更好地装备来校正扰动和错误。**

*****加里斯特尔*** 和 ***国王*** 写着:**

> **从一开始，计算机科学家就意识到强大的计算机的关键特征是速度、效率和可靠性。**

**当在大脑中设计基于反馈回路的记忆机制时，这些问题都没有得到令人满意的解决。自然计算设备的效率使得大脑似乎不可能真的那样运作。记住蚂蚁只有大约 25 万个神经元。上面链接的由 Samsonovitch 和 ***McNaughton*** 建立的简化模型已经需要大约 50 000 个神经元来完成航位推算的工作，如果考虑到蚂蚁还必须做的所有其他复杂事情，这个数字就太高了。大自然不喜欢耗费资源，蚂蚁肯定没多少资源可以备用。**

## **寻找记忆机制**

**这个故事的寓意是，对于许多认知任务来说，执行该任务的计算硬件需要某种类似于可访问的符号记忆机制的东西。当观察蚂蚁外出觅食后导航的效率时，这一点变得很明显。**

**总结一下我们遇到的两个问题:**

*****突触强度****神经网络可能不会真正完成这项工作，因为它们执行计算的方式都是低效的(本质上是通过构建复杂的有限状态自动机，但它们的计算能力有限)，而且存储在它们中的信息是分散的，对大脑本身来说是不透明的。因此，当谈到理解大脑如何计算时，通过调整突触强度实现的联想学习很可能不是全部答案。***

******网络中的循环反馈回路*** 同样似乎不适合作为良好的符号记忆，因为它们能量成本低且容易产生噪声，因此作为长期存储信息的手段并不可靠。***

**Gallistel 和 King 提出，它们太浪费了，不能成为大自然在构建大脑时实际采用的路线，大脑中需要有另一种我们尚未发现的记忆机制。**

**这绝不是说神经元不处理信息，或者信息在某种程度上与它们的活动、位置和连通性无关。这方面的一个例子是海马内位置细胞的作用，由 ***奥基夫*** 和 ***陀思妥耶夫斯基*** 于 1971 年发现(他们因此获得了 2014 年诺贝尔医学奖)。它们的放电与动物(如老鼠)的空间位置有关，它们被认为是地点的认知地图(见[这部动画](https://knowingneurons.files.wordpress.com/2013/04/place-cell-animation.gif?w=1000&h=607,)中的插图)。**

**虽然它们可以为动物如何导航的问题提供更好的答案，但是它们作为路径整合者的功能还没有确定。而且它们也没有解决潜在的读/写符号记忆的问题，这在任何情况下也是许多其他任务 所必需的 ***，我无法在这里介绍(比如间隔计时、学习一天中的时间、或者松鸦获取它们藏起来的食物)。*****

## **为什么认知科学会改变神经科学**

**这就把我们带回了这篇文章的副标题。**

**认知科学研究具有认知能力的设备，更具体地说，大脑，必须如何运行。计算约束表明，大脑作为计算设备的设置必须遵守某些基本原则，这些原则可以告知我们思考大脑神经科学基础的方式。**

*****Gallistel*** 和 ***King*** 提出相关的记忆机制可以驻留在大脑的不同层，例如分子或亚分子层。从物理学的角度来看，神经元绝对是巨大的，人类大约有 ***20 个微米*** ，相比之下，平均原子大小为 ***30 pm*** 。正如费曼所说， ***底部通常有很大的空间*** ，在这六个数量级中(类似于你的体型与纽约和洛杉矶的距离之差)，有很大的潜在空间来建立新的机制。**

**正如我们在 SSD 驱动器、蓝光甚至 DNA 的例子中所看到的，存储信息并不自动预设大量空间和大量资源，并且可以通过更节俭的方式来完成。**

**然而，*和 ***国王*** 并没有提出任何具体的想法:***

> **总之，我们不知道记忆的物理机制是什么。此外，我们拒绝猜测，除了举例说明，它可能是什么。我们拒绝，因为我们相信，面对我们目前的无知水平，我们不可能推测出正确的答案。**

**我认为这非常令人兴奋，因为这表明我们刚刚开始了解大脑的工作。如果我们甚至不知道它是如何存储和处理信息的，我们就无法理解它是如何计算的。神经网络很酷，也是一项伟大的发明，但看起来它们不会为我们提供所有的答案。**