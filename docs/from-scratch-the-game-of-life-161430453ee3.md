# 从零开始:生活的游戏

> 原文：<https://towardsdatascience.com/from-scratch-the-game-of-life-161430453ee3?source=collection_archive---------4----------------------->

![](img/551f031726c093397b22486da00e5513.png)

Source: [Domino Art Work](http://www.dominoartwork.com/life.html)

大家好，欢迎来到“从头开始”系列的第二篇文章。(上一篇:[从无到有:贝叶斯推理，马尔可夫链蒙特卡罗和 Metropolis Hastings，在 python 中](/from-scratch-bayesian-inference-markov-chain-monte-carlo-and-metropolis-hastings-in-python-ef21a29e25a))

在这篇文章中，我们解释并提供了“生活的游戏”的实现。我说“我们”是因为这次我的朋友兼同事 [Michel Haber](https://medium.com/u/15ee6fa2e7df?source=post_page-----161430453ee3--------------------------------) 也加入了进来。我们的两个 GitHub 配置文件中都提供了代码: [Joseph94m](https://github.com/Joseph94m/The-game-of-life) ， [Michel-Haber](https://github.com/Michel-Haber/GoL-hs) 。

第一部分将着重于给出游戏规则的解释以及如何玩/定义游戏的例子。第二部分将提供《生命的游戏》的 Python 和 Haskell 实现细节。在第三部分，我们比较了我们的实现的性能和优雅性。我们选择这两种语言是因为它们代表了两种最常用的编程范式，命令式(Python)和函数式(Haskell)，并且因为它们在编写表达性和可理解的代码方面相对容易。

# 1-生活游戏简介

《生命的游戏》是约翰·h·康威在 20 世纪 70 年代设想的一种细胞自动机，可能是所有细胞自动机中最著名的。尽管规则非常简单，但生命的游戏是图灵完全确定的。

生活的游戏是数学意义上的游戏，而不是可玩的游戏。是“零玩家游戏”。

游戏发生在二维有限或无限网格上，网格的细胞可以采取两种截然不同的状态:“活着”或“死了”。

在每个阶段，单元的演化完全由其当前状态及其八个邻居的状态决定，如下所示:

> 1)恰好具有三个活邻居的死细胞变得活了。
> 2)具有两个或三个活邻居的活细胞仍然活着。
> 3)在所有其他情况下，细胞变得(或保持)死亡。

让我们假设一个简单的初始状态，其中只有 3 个细胞是活的:*左细胞、中间细胞和右细胞*。

![](img/f3d1f9da3b8051a7df256da0bab70ab9.png)

从图 1 中的简单配置开始，让模拟运行一次迭代，结果如图 2 所示。

那么这是怎么发生的呢？

![](img/6231d6ee4c5ae5c08b1ea0d1139e4227.png)

Figure 2

左边和右边的细胞只有一个邻居，中间的细胞，因此它们死亡。中间的细胞有左右两个邻居，所以它还活着。顶部和底部细胞有 3 个邻居(中间，右边和左边)，所以他们变得活跃。值得注意的是，细胞在迭代结束前不会死亡或存活。即算法决定哪些细胞将死亡或复活，然后一起给它们消息。这确保了单元格的求值顺序无关紧要。

再运行一次迭代就会得到图 1 所示的状态(初始状态)。

因此，从这个配置开始，游戏进入图 3 所示的无限循环。这种配置被称为*闪光灯。*

![](img/e0e2ff9f9d455181a940a022cdba7da8.png)

Figure 3: Blinker

![](img/732e3e3d8b9d292c0b3fd05abdc34242.png)

Figure 4: An early state from figure 5 that shows some interesting structures.

现在用一个更有趣的场景来展示给康威印象最深的是什么。从图 5 左图中的简单配置开始，让代码运行，电路板演变成完全意想不到的东西。我们可以观察到稳定的结构:*街区*和*蜂巢。*我们还可以观察到环形结构，例如图 3 中的*眼罩*以及由 3 或 4 个较小眼罩组成的较大眼罩。在这个模拟中观察到的另一个有趣的结构是滑翔机。一架 [*滑翔机*](https://upload.wikimedia.org/wikipedia/commons/f/f2/Game_of_life_animated_glider.gif) 看起来像一架老式电子游戏飞船。它不受空间的限制，继续前进。

![](img/01e62580ff418af0a8938b8b829442fe.png)![](img/ade33092a1257066909f77f1ac0bff71.png)

Figure 5\. Left: Initial state. Right: Evolution

# 2-编码生活的游戏

我们用两种语言实现这个游戏，Python 和 Haskell。我们用这两种语言实现游戏的主要目的，是比较它们在速度和代码优雅性方面的表现。

## 2.1-在 Python 中

在图 6 中，我们定义了**游戏**类。它由一套*规则*、一个*初始状态*和一个*最大尺寸*(宽度和高度)组成。通过调用 run_game 函数并指定最大迭代次数来启动游戏。

Figure 6: Game Class

有两种可能的方式来表示状态:

> 一种密集表示，其中所有单元格都编码在一个宽*高矩阵中。死细胞用 0(或假)表示，活细胞用 1(或真)表示。网格上单元的位置由其在矩阵中的位置定义。
> 
> 只有活细胞被编码的稀疏表示。每个活细胞由它在网格上的位置(int，int)表示。所有这些活细胞都聚集在一个字典结构中。

在我们的例子中，稀疏表示具有优势，因为它需要更少的内存(因为大多数细胞都是死的)，并且允许我们只遍历活细胞集(因为死细胞对它们的邻居没有直接影响)。

无论如何，我们实现了这两种表示，以便提供一个性能基线。然而，为了避免冗余，我们在本文中只展示了稀疏表示的实现。

图 7 显示了稀疏表示的实现。它由一个属性组成，即*网格*，它记录了活细胞在集合中的位置。

Figure 7: State Class

图 8 显示了游戏的规则。在状态的网格上应用规则会返回带有更新的死单元和活单元的网格。

Figure 8: Sparse Rule class

图 9 示出了如何用图 5 的配置运行游戏的例子。

Figure 9: Example how to run the game

![](img/c785085b8857b215e230a7fc738d60a0.png)

Figure 10: The fabulous blaster canon

## 2.2 英寸哈斯克尔

在图 11 中，我们展示了 Haskell 实现的类型定义。我们只实现了稀疏变体。我们利用 *newtype* 包装器来封装我们的主要类型。棋盘或网格只是活细胞坐标的列表。 *TallyState* 是一种状态 [Monad](https://en.wikipedia.org/wiki/Monad_(functional_programming)) 包含我们在其中计数细胞的活邻居的图。

最后， *Rules* 和*neighbors*类型分别表示返回一个单元格的命运及其邻居列表的函数。

Figure 11: Type defiitions

在图 12 中，我们展示了游戏的一组函数。高级功能将规则应用于当前状态，并返回新状态。

Figure 12: The simulation functions

最后，在图 13 中，我们实现了我们的主函数和标准规则。

Figure 13: Main

# 3-比较

如前所述，我们想要比较不同表示的速度和优雅程度。

## 3.1-不同设置、电路板尺寸和初始配置的处理时间。

**对于 80x80 的板尺寸，迭代 1500 次，初始配置为(39，40)，(39，41)，(40，39)，(40，40)，(41，40)。结果如图 14 所示。相应的计算时间为:**

> Python，密集:150 秒
> 
> Python，稀疏:1.03 秒
> 
> Haskell，稀疏:0.475 秒(使用-O3)

![](img/ade33092a1257066909f77f1ac0bff71.png)

Figure 14.

**在我们的第二次测试中，我们使用了 200x200 的电路板，并从以下初始配置开始运行 2000 次迭代模拟:**

**(50180)、(51180)、(50181)、(51181)、(60180)、(60179)、(60181)、(61178)、(62177)、(63177)、(61182)、(62183)、(63183)、(65182)、(66181)、(66180)、(66179)、(65**

**这导致了我们在图 15 中看到的结果，相应的计算时间是:**

> Python，密:1456 秒~ 24 分钟
> 
> Python，稀疏:1.54 秒
> 
> Haskell，稀疏:0.802 秒(使用-O3)

![](img/c785085b8857b215e230a7fc738d60a0.png)

Figure 15.

从这两个测试来看，很明显 Python 中的密集表示比 Haskell 和 Python 中的稀疏表示要慢得多。这种行为是意料之中的，因为密集表示(a)单独处理单元，(b)试图评估死单元对附近单元的影响，即使已知死单元不会影响附近单元的未来状态，以及(c)使用更多的存储器，因为它存储所有单元的状态——这可能不会对这两个测试的速度产生直接影响，因为板的尺寸不是很大， 但是如果程序不能再在内存中容纳主板，那么它必须进行磁盘交换，这将进一步增加完成运行所需的时间。

在提供的两种稀疏表示中，Haskell 表示在计算时间上有显著的改进。

## 3.2-编程优雅

评估实现的优雅程度是一项相当主观的任务。相反，我们建议显示两种实现的一些指标:有效的代码行、函数的数量和显式条件语句的数量。

因此，代码优雅在很大程度上依赖于个人喜好，我们因此将决定权留给读者；)

**有效代码行数:**

> 密集 Python 表示:~75
> 
> 稀疏 Python 表示:~70
> 
> 稀疏 Haskell 表示:~40

**功能数量:**

> 密集 Python 表示:6
> 
> 稀疏 Python 表示:6
> 
> 稀疏哈斯克尔表示:7

**显式条件语句的数量:**

> 密集 Python 表示:13
> 
> 稀疏 Python 表示:11
> 
> 稀疏 Haskell 表示形式:0

# 4-结论

最后一个模拟，我们显然没有做:)。模拟人生游戏的人生游戏。

[https://www.youtube.com/watch?v=xP5-iIeKXE8](https://www.youtube.com/watch?v=xP5-iIeKXE8)

A game of life, within a game of life.

有趣的是，看到如此复杂的系统可以从这样的基本规则和配置中出现——这让我们想起了现实世界，在现实世界中，基本单元聚集在一起，产生更加复杂的结构，如生命。

关于我们的两个普通(ish)实现，Haskell 实现在速度(和优雅性)上优于 Python 实现。).也就是说，人们可以想象其他一些 Python 和 Haskell 实现会带来更好的性能和代码优雅性。

最后，感谢您的阅读，不要忘记亲自尝试代码！