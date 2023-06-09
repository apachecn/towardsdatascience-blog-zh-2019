# 深度学习中的“深度”——一种实用方法

> 原文：<https://towardsdatascience.com/fathoming-the-deep-in-deep-learning-a-practical-approach-c18adab31cbe?source=collection_archive---------16----------------------->

“深度学习”是难以捉摸的，但只要有一点数学知识就可以接近。这引发了一个实际问题:初等微积分足以解释深度学习吗？答案确实是肯定的。带着无限的好奇心去学习和重新学习新的和旧的，如果你能有条不紊地遵循下面的章节，我认为你会跨越鸿沟，直观地理解和应用每一个概念，包括微积分，以消除深度学习的所有复杂性。

学习“深度学习”既有趣又令人担忧。数学是基础，可以帮助清楚地理解和不可磨灭地蚀刻概念。当我开始阅读迈克尔·尼尔森的书[“神经网络和深度学习”](http://neuralnetworksanddeeplearning.com/chap1.html)时，我一开始不小心完全理解了许多需要复习的基本概念，我想如果我可以与他人分享我的旅程以简化他们的学习，那么我想我已经为促进深度学习尽了自己的一份绵薄之力。

在这篇文章中，我将讲述我所采取的步骤以及我所研究、阅读和理解的内容——尽可能直观地揭示每个概念以及引起你兴趣的其他主题。每一步都在一个标题下详述，以理解深度学习的整个架构，这是仍在发展的人工智能的基石。随意跳过熟悉的部分，深入研究感兴趣的内容。

测量深度的步骤:

1.  [开端——用感知器模拟决策](https://medium.com/p/c18adab31cbe#5b07)
2.  [节点内部的主力——激活功能](https://medium.com/p/c18adab31cbe#060d)
3.  [稍微绕了一下基础——微分学](https://medium.com/p/c18adab31cbe#72d9)
4.  [基础——基本统计和损失减少](https://medium.com/p/c18adab31cbe#a43d)
5.  [大优化—梯度下降](https://medium.com/p/c18adab31cbe#aeb3)
6.  [救援直观示例—下降揭秘](https://medium.com/p/c18adab31cbe#6c97) d
7.  [系综直接向后&向前—前馈&反向传播](https://medium.com/p/c18adab31cbe#e746)
8.  [Bare neural net 的内部工作——与代码匹配的矩阵](https://medium.com/p/c18adab31cbe#1c5e)
9.  [学习曲线回溯—参考文献&致谢](https://medium.com/p/c18adab31cbe#8373)

# 开始——用感知器模拟决策

[榜首](https://medium.com/p/c18adab31cbe#99222)

生物神经元模型解释了神经系统促进感知(无论是感觉还是其相关活动)的潜在机制。从这种感知中产生了“感知器”,一种寓言式的数学单位或模型。简而言之，感知器(1)接受多个输入，(2)加权(乘以一个设定的权重)，(3)求和并累加到一个称为 bias 的常数，最后(4)发送到一个激活函数以(5)提供一个输出。

通常你可以把感知机想象成一个数学模型，在给定一组输入和一个阈值的情况下，决定我今天是否可以去看电影。假设输入是云量、假日事件、一天中的时间，所有这些都是一个按比例缩放的实数，每个都通过乘以相应的预设权重进行修改，并与阈值(偏差因子)相加，然后这个组合数被步进或平滑，其中步进函数的结果是 1 或 0，而平滑函数的值在 1 或 0 之间，这可以解释为结果发生的概率。

为了清楚起见，下面是上面例子的一个说明:

![](img/01329d63f00d7730bf5dcfa400654b66.png)

从数学上来说，如果我们有 j 个感知器输入，输出表示为:

![](img/48f141dc5e9577c757581588ae303828.png)

为了进一步简化，我们可以将上面的等式视为点积或标量积，这是一种代数运算，采用两个等长的数字序列(通常是坐标向量)并返回一个数字。两个向量 **w** = [ *w* 1、 *w* 2、…、 *wn* 和 **x** = [ *x* 1、 *x* 2、…、 *xn* 的点积定义为:

![](img/6cd4af65ede66df7d7323f8038221a98.png)

以这种方式表达上面的例子，一个 1 × 3 矩阵(行向量)乘以一个 3 × 1 矩阵(列向量)得到一个 1 × 1 矩阵，用它的唯一条目来标识:

![](img/ab0cf33242008819ca0613b6af5a8366.png)![](img/75323b65352b142f4f0870c53db49f7e.png)

从上图中，我们可以直观地将感知器网络想象成一个可以连续过滤前一层的网络，即，对前一层的决策进行加权和决策，以此类推，直到我们到达作为输出的最后一层。有时，输入可以被表示为一个感知器，只有一个固有的或恒定的偏差，没有权重或指向它的输入。早期，当感知器模型被创建时，人们认为 NAND 或 XNOR 不能被模拟，这使得创新的步伐处于休眠状态，后来人们发现所有的位运算都可以被模拟，或者事实上是展示任何模式的函数。随着多层网络变得明显，深度学习终于打破了它的休眠，并迅速收拾残局。

# 节点内部的主力—激活功能

[顶部](https://medium.com/p/c18adab31cbe#99222)

对任何过程建模都是测量输出与给定输入的基本活动，以获得理解，更重要的是保证在已建立模型的情况下给定输入的结果的可重复性。本质上这个模型对我来说总是用简化的术语来说就是“曲线拟合”。有了输入和模型，您总是可以确定输出是什么。激活函数是“曲线拟合器”,在给定输入的情况下，它们根据定义的模型提供输出。同样，模型的变化导致不同的激活函数。

# 步进功能

一个基本的激活功能是步进功能，如下图所示:

![](img/e99d574d6985106845009da01757e8fc.png)

方程式:

![](img/23152b7bb0ffc16ee89b48485a6b4bb6.png)

步进器或二进制是一个输出为 1 或 0(是或否)的函数。或者，它也被称为 [Heaviside](https://en.wikipedia.org/wiki/Heaviside_step_function%E2%80%9D>Heaviside) 阶跃函数或单位阶跃函数。该函数为所有负输入发出 0，为所有正输入发出 1。感知器使用这种激活来根据输入发出是否继续的信号。

# 线性函数

顾名思义，线性函数将给定的输入增加一倍。数学上，线性函数是其图形是直线的函数，即一次或零次多项式函数。

![](img/611fc614cb6275052f16944f8b92bb9d.png)

方程式:

![](img/76025746e5bc335c010701f71c8aa31f.png)

该图表示线性函数 f(x) = 4x，本质上对输入有 4 倍的乘数效应。每当我们想要按比例缩放输入时，这在神经元中是有用的，但是它的用例很少。

# Sigmoid 函数

Sigmoid 是一条 S 曲线，其中所有正值的输出都= 0.5，输出永远不会超过 1。对于 x 轴和-x 轴的较高值，y 值是一个[渐近线](https://www.mathsisfun.com/algebra/asymptote.html)。S 形的顶部是凹的，底部是凸的。sigmoidal 函数的定义非常广泛，但唯一的是它有一个实值输出，一个拐点和一个钟形一阶导数。

![](img/00ac23e1309aff4daaae012675fa3f33.png)

方程式:

![](img/238fcd755936aa68d204dd30b20295f6.png)

一般来说，Sigmoid 函数是从逻辑函数获得的，逻辑函数的常见形状是“S ”,其等式为

![](img/9c30bdb376fc03b84a25b3e8c691df01.png)

在哪里

*   e =自然对数底(也称为欧拉数)，
*   x0 =形中点的 x 值，
*   L =曲线的最大值，以及
*   k =曲线的逻辑增长率或陡度

在标准逻辑 sigmoid 函数的情况下，值将如下:L = 1，k = 1，x 0 = 0，给出上面的 Sigmoid 方程。

![](img/a312ab3103e822248e511db688b992d8.png)

。这个函数的一个很大的优点是它是非线性的。在-3 和 3 的范围内显示线性，在该范围的其余部分逐渐变细到渐近线。它可用于将连续空间值转换为二进制范围之间的值，这种离散化方法对于抑制极端情况非常有用，其特征是在低激活时极限值为零，在高激活时极限值为一。目前，这个函数足以开始我们的神经网络之旅，但我们稍后将全面探讨其他函数及其适用性。

## Sigmoid 优化背后的理念

对 sigmoid 的兴趣在于它可以在同一个函数中管理线性和非线性建模。在上图中，拐点在 0.5 处，由 z 表示。Sigmoid 曲线模拟了典型的规模经济问题。例如，如果制造商开始制造玩具，初始投资很大，回报率很低或接近于零，一旦公众开始购买玩具，销售额逐渐增加，并随着需求的增加而呈线性增长，此时供应不能完全满足需求，利润飙升至供应赶上需求的拐点，此时利润理想，供应超过需求，无论施加多大的影响，利润率都会下降，不能超过最大值。

这推测任何依赖于阈值的活动都是通过 sigmoid 函数进行优化的理想候选。让我们看看几个这样的候选对象，并将其与它如何帮助深度学习用例联系起来。如果竞选经理试图优化他们的广告支出，那么他们的目标函数将模拟一个结果，在这个结果中，他们希望把钱花在可能改变投票支持他们的候选人的州上。而花在最终失败的州上的钱则完全浪费了。Sigmoidal 函数也会以同样的方式运行，只建议在一个州花钱，如果他们能通过获得大多数选民的门槛。他们会预测，在一个很有可能受到影响的州投入大量资金，要比在两个州各投入一半资金要好，因为在这两个州，他们最终可能会两败俱伤。在从给定图像预测数字的“深度学习用例”中，每个像素或像素组共同跨越一个阈值将是有用的，如果使用分层 sigmiod 函数连续交叉验证它们，那么它可以以更少的错误完美地预测结果，并且在此过程中，我们的模型将学习得很好。

# 关于基础的一个温和的迂回——微分学

[榜首](https://medium.com/p/c18adab31cbe#99222)

# 区别

在我们深入研究之前，我们必须回忆一下我们在高中数学中学习的关于微积分的知识——这对我们外行的大脑来说是一个可怕的主题，那么，这是一个带着乐趣和功利主义心态进行反思的完美时间，而不是我们在学校时代所做的死记硬背。

衍生品就是变化率。你从家到目的地需要多长时间？这些年人口增长有多快？人们有多富有？所有这些都在谈论变化率，一个对另一个。与上面的例子相比，它们是距离对时间，计数对年，美元对人计数。

顺便提一下，变化率也是斜率，如果将上述用例数据之一绘制在 x-y 轴、y 轴上的距离和 x 轴上的时间的图表中，则两个时间点之间的平均速度由所用时间内行驶的距离给出，这实际上就是斜率。如果你真的想找到某个特定时间点的速度，很难测量在无限小的时间片上走过的距离，因此没有办法计算变化率。但是差异化在这里很有帮助。

受到对复杂数学概念的清晰而简单的解释的启发，让我们借用一下学习的概念(感谢 MathIsFun site，by Ed。罗德·皮尔斯)以更清晰、有趣和简洁的方式解释衍生品。请确保你仔细阅读了每一篇文章，以回忆/刷新你当时所学的内容，并将微分学内化，这对理解神经网络的功能是至关重要的。

1.  [导数介绍](https://www.mathsisfun.com/calculus/derivatives-introduction.html) —讲述变化率，它与斜率的关系，我们如何得出给定函数的斜率
2.  [导数规则](https://www.mathsisfun.com/calculus/derivatives-rules.html) —涵盖管理各种类型函数导数的规则。
3.  [幂法则](https://www.mathsisfun.com/calculus/power-rule.html)——将幂函数去杂波的最简单方法
4.  [二阶导数](https://www.mathsisfun.com/calculus/second-derivative.html) —理解速度、加速度和加加速度的二阶导数的绝妙方法
5.  [偏导数](https://www.mathsisfun.com/calculus/derivatives-partial.html) —实际使用案例，使用我们熟悉的圆柱体了解偏导数的真实用途
6.  [可微分](https://www.mathsisfun.com/calculus/differentiable.html) —该测试允许检查曲线的可微分性，以确定斜率的存在
7.  [使用导数寻找最大值和最小值](https://www.mathsisfun.com/calculus/maxima-minima.html) —学习梯度下降和反向传播的基础

# 微分就绪计算器

![](img/d0868290727b68eaec0e8d2f90d947e9.png)

Image Credit: MathIsFun

![](img/3e5548d4e86419e451d187e6580c5d03.png)

Image Credit: MathIsFun

[如何理解衍生品:积、幂&链规则](https://betterexplained.com/articles/derivatives-product-power-chain/) —提供了一种直观的方式来理解我们在高中时一直记忆的**积、幂和链**规则。有了对微分学的坚定理解，我们再下一步！

# 基础——基本统计数据和减少损失

[顶端](https://medium.com/p/c18adab31cbe#99222)

# 统计数字

在统计学中，您应该熟悉对位置和可变性的估计，这对于数据如何表示和变化以及如何缩放数据以实现标准化和加快分析至关重要。与这一“深度学习”之旅相关的基本概念的快速总结:

## 位置估计

具有测量数据的变量可能有数千个不同的值。探索数据的一个基本步骤是获得每个特征(变量)的“典型值”:估计大部分数据的位置(即它们的集中趋势)。

*   **表示** 所有数值的总和除以数值的个数
    替代:平均值
*   **加权平均值** 所有值的总和乘以一个权重除以权重的总和。
    替代:加权平均
*   **Median** 使一半数据位于上下的值。
    备选:第 50 百分位
*   **加权中值** 使权重之和的一半位于排序数据上下的值
*   **稳健** 对极值不敏感。
    替代:抗性
*   **离群值** 与大部分数据差异很大的数据值。
    替代:极值

## 可变性的估计

位置只是概括一个特征的一个方面。另一个维度是可变性，也称为离差，衡量数据值是紧密聚集还是分散。统计学的核心是可变性:测量可变性，减少可变性，区分随机可变性和真实可变性，识别真实可变性的各种来源，并在存在可变性的情况下做出决策。

*   **方差** 
*   **平均值绝对偏差
    平均值与平均值偏差的绝对值的平均值。**
*   **范围
    数据集中最大值和最小值之差。**
*   **百分位数** 该值使得 P 个百分比的值等于或小于该值，而(100-P)个百分比等于或大于该值。
*   **四分位距** 第 75 个百分位和第 25 个百分位之差

## 数据缩放

来自[维基百科](https://en.wikipedia.org/wiki/Feature_scaling):由于原始数据的取值范围千差万别，在一些机器学习算法中，目标/损失函数如果不进行归一化将无法正常工作。例如，大多数分类器通过欧几里德距离计算两点之间的距离。如果其中一个要素的值范围很大，则距离将由该特定要素决定。因此，应该对所有要素的范围进行归一化，以便每个要素对最终距离的贡献大致成比例。

应用要素缩放的另一个原因是，使用要素缩放时，梯度下降(我们稍后将更详细地了解这一点)的收敛速度要比不使用要素缩放时快得多。

*   **mix-Max 的最小-最大缩放比例** 公式:

![](img/5606cf55c7511294f8f38eb8e033a1b3.png)

这种方法在一个范围内(比如[0，1])重新缩放单个数据点。假设我们有一个包含 100 个数据点的数据集，x 是一个单独的数据点，min(x)是 100 个数据点中的最小值，max(x)是其中的最大值，min-max 缩放将每个 x 值压缩(或拉伸)到范围[0，1]内。有时该范围可以设置为[-1，1]。目标范围取决于数据的性质和分析中采用的算法。下图给你一个直观的说明。

![](img/ee1edf326ba6035ed81d5c3ace86a1cf.png)

Image Credit : Feature Engineering by Alice Zheng

**单位换算或 L2 归一化** 单位换算公式:

![](img/b7db717c33533cb35d166f746b696436.png)

这是通过将每个数据点除以距离中心或平均点的向量的欧几里德长度而获得的。L2 范数测量坐标空间中向量的长度。勾股定理给出了距离

![](img/0eaf4e4d446f149eca34b5f4fc1fa993.png)

由于这种划分，数据在-1 到 1 的范围内正常化。

![](img/8417dfebc667810ba5a3025073d4dafd.png)

Image Credit : Feature Engineering by Alice Zheng

**方差缩放或标准化** 标准化公式:

![](img/f1f593aa9ac15c31e8496a65ae3e0cd8.png)

平均值直观地表示数据的绝对分布，而标准差(SD/sd)给出了加权分布的概念。当数据的分布围绕平均值对称，并且其方差相对接近正态分布时，分布的度量是最有用的。(这意味着它是近似正常的)。在数据近似正常的情况下，标准偏差有一个规范的解释:68%的数据将在 1 个标准差内，95%在 2 个标准差内，99%在 3 个标准差内。问题是分布是宽还是紧？这给出了数据和可能出现的异常值的概念。
在这里，对于每个数据点，平均值被去除，并通过它们的标准偏差进一步加权。从本质上来说，是根据数据点的总体分布来调整每个数据点的中心值。
得到的缩放数据点被标准化为平均值为 0，方差为 1。如果原始特征具有高斯分布，则缩放后的特征是标准高斯，也称为标准正态。下图直观地说明了这个概念。

![](img/22902b193ac3ff5fd1a45c07c5dad79e.png)

Image Credit : Mastering Feature Engineering by Alice Zheng

# 损失函数

可变性激发了预测偏差的测量方式，与标准偏差类似，损失可以被测量、缩放和标准化。损失函数的核心是衡量你的预测与原始值相比表现如何。现在，您有了一个工具来跟踪模型性能，同时调整其性能，以便将损失降至最低。非常基本的损失函数是找到原始值和预测值之间的绝对差值。这提供了对单个预测的良好判断(绝对误差— AE ),并且同样可以对所有预测进行平均，以获得平均绝对误差(MAE / L1 损失),并且平均它们的平方误差给出均方误差(MSE / L2 损失/二次损失)。

## 中小企业与制造业——一项分析

我们来取一个简单的函数 y = f(x) = 4(x)，针对这个函数画一个图如下。还绘制了相应的预测值 y，以显示与实际值的偏差以及损耗、绝对损耗和平方损耗。还给出了统计值以及平均误差和均方误差。

![](img/ad6857a93412d158f7d88d3f6b86934c.png)

这些公式是:
MSE=

![](img/9e6220e88b45adefefaf320db36f9612.png)

MAE=

![](img/15967ef21d56c6bd6823d81e47547a90.png)

y^p=预测值(predicted)，y =观测值(actuals)。

如果公式不是你的主食，你可以通过
**MSE** 找到 MSE & RMSE

*   平方残差/损失。
*   求残差/损失的平均值。

**RMSE**

*   取结果的平方根。

MAE 和 MSE 都表示在不同的感兴趣单元中的平均模型预测误差稍有不同。这两个指标的范围从 0 到∞并且与方向误差无关。它们是负校准分数，这意味着值越低越好。取平均平方误差或简单平方误差的平方根有一些有趣的含义——因为误差是平方的，并且在它们被平均之前，MSE/RMSE 给大误差一个相对高的权重。这意味着当大误差特别不理想时，MSE/RMSE 应该非常有用。

查看上图，我们可以看到实际值和预测值的 MAE 和 MSE (RMSE 就是 MSE 的平方根)值。除了误差非常高的 2 个异常值之外，大多数预测是内联的。与 MAE 相比，MSE/RMSE 将会给异常值很大的权重，因为你会注意到平方损失远远高于他们更接近的损失。直观地，我们可以从损失函数角度解释预测性能，其中如果试图最小化 MSE，那么预测应该是所有目标值的平均值。但是如果我们试图最小化 MAE，这个预测将是所有观测值的中间值。中位数比平均值对异常值更稳健，这使得 MAE 比 MSE 对异常值更稳健。

使用 MAE 损失(特别是对于神经网络)的一个大问题是其梯度始终相同，这意味着即使损失值很小，梯度也会很大。这对学习没有好处。为了解决这个问题，我们可以使用动态学习率，它随着我们接近最小值而降低。MSE 在这种情况下表现很好，甚至在固定的学习速率下也会收敛。对于较大的损失值，MSE 损失的梯度较高，并且随着损失接近 0 而降低，使其在训练结束时更加精确(见下图)。)

**MAE 损失**

![](img/33e5a1bf94903c011fae9a0c31d205b8.png)

Image Credit: Heartbeat — MSE & MAE Loss

**MSE 损失**

![](img/e712a733dc5858942cc5092cac9a261e.png)

上面是 MAE & MSE 函数的图，其中真实目标值为 100，预测值的范围在-10，000 到 10，000 之间。MSE 损失(Y 轴)在预测值(X 轴)= 100 时达到最小值。范围是 0 到∞。

# 神经网络中的一些损失函数

损失函数在稳定和提高给定模型的预测精度方面起着至关重要的作用。它们被用于将实际值和预测值之间的差异最小化。下面列出了深度学习中使用的损失函数的总结——名称、方程和它的作用要点。

请注意，y 是实际点或节点数据，yhat 是 y 的预测或函数输出，C 是所有数据点的总误差。

![](img/c2a7fd42c77b0cdb2aebd59490d38c33.png)

在回归中广泛使用，数据点的合成拟合线应该是使每个点到拟合回归线的距离总和最小的线。实际值和预测值之间的平方差称为“残差”,损失函数的目标是最小化 DL 中的残差平方和。

![](img/62e86da64f819e4183f46ed5d2285021.png)

顾名思义，它是 MSE 值的一半，这是为了方便计算，我们稍后会讲到。

![](img/d98cb580e15f76cc43609d0233babfab.png)

简单地求和，不求均方误差的平均值。也叫 L2 损失

![](img/6f84942d1bec9d5195ffa0d432f575b9.png)

它测量实际和预测的对数值的方差差异。当预测值和实际值都很大时，这很有用-使用对数的力量将指数值减少到渐进值。MSLE 对低估的惩罚多于高估。

![](img/9043aa054e1579bbb559f84d2a14d031.png)

实际值和预测值之间的绝对差值。用 MSE 计算一个好的梯度更容易，而 MAE 只给出一个常数。

![](img/4fe27ad0e0de7315aebfb47c8b743660.png)

很明显，实际值与预测值的百分比误差超过了实际值。当实际值为零时，不能使用。当实际和预测之间的差异很大时，它会超过 100%。该函数倾向于选择预测值过低的模型。

![](img/18fe4fb98298292f382f40a44dd75d14.png)

MAE 没有平均值，即没有除以 n

![](img/80a3349801891c8c4466ab614656f3dc.png)

通常在二进制分类和神经网络中，输出是表示预期结果的概率的真实值，而不是给定事件的 0 或 1。或者可以很容易地计算出来——给定一组数据点，测井曲线损失衡量实际与预测的概率分布的差异。我们还可以假设实际数据点和预测数据点代表一种概率分布。从二进制分类的角度来看，y 是事件 A 或 B 的非此即彼标签(如果 A 发生，则为 1；如果不发生或 B 发生，则为 0 ), p(y)是其概率。左手边代表，标签乘以标签为 A 的概率，而右手边 1-标签值乘以为 b 的概率。进一步的直观解释[此处](/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a)和参考[此处](https://deepnotes.io/softmax-crossentropy)为从 softmax 导数的良好推导。

![](img/95303891430cd42aa1b1b2e6c4b3bce5.png)

当模型输出是每个类别的概率而不是最有可能的类别时-其中它处理多类别，即每个输出将表示例如每个输出是猫、狗还是老鼠。Lj Miranda 博客中的[理解 softmax 和负对数似然](https://ljvmiranda921.github.io/notebook/2017/08/13/softmax-and-the-negative-log-likelihood/)是一篇关于 soft-max 和 NLL 的好文章。我完全被那篇文章中的精彩画面迷住了。

![](img/0a6301c473f64e814caa8b4ebaaae291.png)

Image Credit: Lj Miranda Blog

![](img/820e187ac8d2da06aa6cc3c9e2ef42d1.png)

将以上两者联系起来，直接阅读直观的[文章](/demystifying-kl-divergence-7ebe4317ee68)以获得简洁的解释。

![](img/49b583a153e4f27f4e5eb77f6dbf45cd.png)

从高中开始，我们知道 Cos 0 是 1，Cos 90 是 0，这表明余弦接近于 0 的给定的一组点比接近于 1 的点相似，在 1 的点上它们是完全发散的。这样可以忽略幅度差异，只考虑角度收敛。

损失及其对误差减少的影响以及与梯度下降的比较在[这里](https://heartbeat.fritz.ai/5-regression-loss-functions-all-machine-learners-should-know-4fb140e9d4b0)详细讨论。接下来我们将更直观地处理梯度下降。

# 大优化—梯度下降

[榜首](https://medium.com/p/c18adab31cbe#99222)

# 梯度下降

在提到 ML/DL 时，经常提到的算法是梯度下降法。因为它是如此的基础，所以大部头的书都已经涵盖了对它的说明、解释和驳斥，但是这里我们将通过两个例子来更直观地理解它，而不是你遇到的花哨的 3D 图表和动画。

在我们深入研究一个例子之前，梯度下降字面上是“一种穿越的方式”,这样我们就到达了谷底。形象地说，我们必须下降，并检查我们是否在最低处，如果不是，寻找下一个最佳下降方向，并重复迭代。一个警告是，如果我们被困在一个最低的最小值，但不是最低的(假设我们有一个可以看穿岩石的激光视力)，然后折回并开始在将导致最低最小值的方向，全球最小值在谷底深处，谷底点。

假设我的山谷没有扭曲，是一维的，看起来像代表 y = x^2 的曲线，那么我们可以在下图中画出这个山谷。回想之前使用一阶和二阶导数找到[最大值和最小值](https://avantlive.wordpress.com/2019/04/29/fathoming-the-deep-in-deep-learning-a-practical-approach/)的过程。这里，斜率向右增大，向左减小。参考两条曲线，第一条是曲线 y = x^2，下一条是曲线 y = 1+2x-x^2.下图说明了这个想法。

**了解坡度&在基本曲线上下降**

![](img/ce8556a3c9b9ca5a41f7469d190c6485.png)

正如我们注意到的，在上面的左图中，斜率是正的，并且随着我们向右移动而增大，随着我们向左移动而减小。为了找到全局最小值，这是一个简单的操作——在斜率图中直观地查看斜率达到零的位置，或者在数学上，如果斜率方程等于零，我们得到 x = 0，斜率最小的点是全局最小值。你可以在 x (=0)，二阶导数= 2 这一点上应用二阶导数测试，当它大于 0 时，它是局部最小值，并且是一维的，它也是全局最小值。还要注意没有迭代过程，因此一维函数本身没有梯度下降。同样，右图给出了一个想法，当我们冒险寻找全局最大值时，抛物线方程会发生什么。这里，二阶导数= 2–2x，当 x = 1 时，斜率为零。应用二阶导数测试，在这一点上是-2，我们知道这是一个一维函数的局部最大值，也是全局最大值。

![](img/d1910fbbb6c25319ff17172dc9bcd697.png)

二阶导数不可能为零，除非 y = x(如上图所示),这里斜率是常数，没有最小值或最大值点，而是一个技术上未确定的点，称为鞍点。鞍点发生在多维函数中。

另一个重要的直觉是，在一维函数中，我们向左或向右移动，但从另一个角度来看，如果当斜率为正时，你向相反方向移动，你将达到最小值，即当斜率在某一点最陡时，然后向相反方向移动，陡度降低并达到零。这在多维函数的梯度下降中很方便。为什么重要——我们可以简单地将该点的最陡斜率乘以一个小因子，然后减去/加上，将 x 轴点向相反方向移动，并重新评估函数的斜率，看它是否变得不那么陡，并达到最小值，然后重复这一过程，直到达到最小值。

# 救援的直观例子——下降揭秘

[榜首](https://medium.com/p/c18adab31cbe#99222)

# 简单函数 f(x，y) = x + y 的梯度下降

是时候回忆一下我们之前研究过的[偏导数](https://avantlive.wordpress.com/2019/04/29/fathoming-the-deep-in-deep-learning-a-practical-approach/)了。如果 f(x，y，z)= x ^ 4-3 XYZ，那么用卷笔字表示法:

![](img/185249a90338ba8643dca4b710892c64.png)![](img/cbb88363bfa650df201a782d893f7f6b.png)![](img/2715f7ba1907f38b132b547544906856.png)

现在让我们考虑一个函数 f(x，y) = x + y。将 x 和 y 的值分别初始化为 2 和 4，输出将是 6。

这里招手的是，如何调整 x 和 y 的值使泛函输出最小？公式很简单:

*   新 x 位置=旧 x 位置—(小常数)* fn w . r . t x 的斜率
*   新 y 位置=旧 y 位置—(小常数)* fn w . r . t y 的斜率

![](img/f244f650a37dac6ca0a646fec08cc014.png)

让我们用它的分量来区分 f(x，y)

![](img/0b663123e12ca06459a81254477f4d35.png)![](img/7f7ee6fa9e8ccdd1cbd21036afbecc44.png)

这些偏导数可以被认为是作用在 x 和 y 输入上产生输出的力。当我们产生输出时，目标是达到最小或零输出(顺便提一下，此时 x 和 y 的斜率为零，二阶导数为+ve——回想一下我们之前的最小值/最大值探索，这里的输出和损失函数也是一样的)。让我们看看如何应用上述公式，我们假设 delta = 0.01。

![](img/6bc249c2fad65522df8f7e1a780beafd.png)![](img/27b59071c2766fdc15de8912fdd4dfbe.png)

x 和 y 的新位置导致 f(x，y) = x + y 的值为@ 1.99 + 3.99 = 5.98。与我们的起始值 6 相比，它略小。为了达到值 0，我们将利用梯度下降的重要特征，即迭代步骤，直到我们达到收敛。过程是重复的

![](img/01ff5bfab455a418771fb1e1f82ad1fe.png)

直到 x+y 为零。因此，如果我们重复上述步骤 300 次，我们将得到 x = -1 和 y = 1，最终输出 x+y = 0，我们最终得到的 x 和 y 的值将给出最小值 0。

# 函数 f(x) = mx + C 的梯度下降

让我们举一个简单的例子，沉浸在内部工作，因此可以清晰地上升梯度下降。

![](img/e07399af63eafe2a98273fbe8f66dc1f.png)

根据在城市中央商务区(CBD)进行的一项调查，收集并在*栏 A* 和*栏 B* 中列出了办公空间租金价格，分别确定了以平方英尺为单位的办公空间面积(X)与以千美元为单位的每月租金收益率(Y)。

问题陈述:对于 CBD 的一个新办公空间，给定建筑面积，每月租金收益是多少？

![](img/384a1e7d1889eeea7b25d61620d4e7ba.png)

绿线描绘了当前收益率价格与地板覆盖面积的关系。我们将使用一个简单的线性模型来预测给定其建筑面积(X)的新租金收益率(Y pred)。琥珀色线描述了预测给定区域产量的模型

Y pred = mx + C

绿线给出了基于当前调查的实际租赁收益(Y actual)。

绿色点和琥珀色点之间带有互连线，表示 Y 实际值和(Y 预测值)之间的差异，即预测损失或误差(E)。
我们有责任找到 C 和 m 的最佳值(称为权重),使其最适合 Y pred = mX + C 支配的预测线，以减少预测误差并提高准确性。我们将采用二次损失函数 RMSE 作为损失函数，考虑到实际值和预测值，需要将其最小化。

简单的说 HMSE =，

![](img/54f95c577dacbefadb5374c1823c82c1.png)

让我们利用梯度下降算法来找到权重 C 和 m 的最佳值，以最小化 HMSE。

这里列举了所涉及的步骤:

1.  使用最小-最大归一化法将 A 列和 C 列中的数据分别归一化到 D 列和 F 列中，并将用作 X 和 Y
2.  将 C 和 m 初始化为随机值，并计算每个数据点的平方误差(SE)
3.  当 C 和 m 相对于原始随机值变化很小时，单独计算每条线/数据点' HMSE 变化',总变化构成所有数据点所有这些变化总和。
    *求和后，我们可以将求和值除以数据点数来求平均值，但这是不必要的，因为它只是缩小了总变化，而且会影响我们随后引入的变化，如下一条语句所示。本质上，这可能会减慢收敛速度，因此我们可以停止 ar 求和，无需求平均值。在动态情况下，输入数据点的数量事先不知道，那么我们也不能平均，因此最好是左总结*
4.  调整相应的权重 C 和 m 减去乘以学习率的总“HMSE 变化”
5.  使用新的权重来计算 se 的总量，并检查它是否在减少
6.  重复步骤 3 和 4，直到总硒不再显著减少

详细步骤:

1.  参考*列 D、E&F*——它们是对应于*列 A、B & C* 的最小-最大归一化租金数据
2.  要拟合 Y pred = C + mx 线，首先使用随机种子值并计算预测损失 HMSE。HMSE 在所有数据点上，当应用于单个数据点时，公式中的 n 被去掉——只需计算出每个数据点的半平方误差，然后求和。SE 和 HSME 在这方面指的是同一个。

![](img/7e2972514313ff10e5a0b6a2beb80c46.png)

[**下载源 Excel**](https://avantlive.files.wordpress.com/2019/04/activation-functions.xlsx)

3.计算重量的误差梯度 w.r.t，在我们的例子中是 C 和 m

![](img/bde9632a3467362f2f5aae21dd3ac100.png)![](img/96f617ea1e7fa0020aad4feef3b6168d.png)![](img/065a61b35feee6e5018054d0841ff570.png)

我们稍后将分别对上述方程进行演算。上述两个等式给出了“C 和 m”的变化，并且是简单的梯度，其将运动方向从 w.r.t .指向 SE。参考最后两栏的计算

4.用梯度改变权重 C 和 m，以达到最小的最佳 SE 值。

![](img/603d9bae3ed773bdc0c1c84159f73d75.png)

我们将调整 C 和 m 的初始随机值，使我们朝着最优 C 和 m 的方向前进。

![](img/23683170e1eae801eba678254d517fba.png)

*更新规则:*

![](img/22af55378a6bde0483ec04b37d868938.png)![](img/55a5c42a6c1f9a2eaf31d5625b057e1b.png)

*这里 lr 是学习率，因此:*
New C = 0.52–0.01 * 5.040 = 0.47
New m = 0.81 = 0.01 * 2.279 = 0.79

5.使用新的权重来计算 se 的总和并检查其是否减少-检查上图中 HSME 值 id 的总和是否减少

6.随着步骤 3 和 4 的重复，直到总 SE 不再连续显著减少，然后我们达到了具有最佳预测率的最佳 C 和 m

# 梯度下降背后的微积分

## 平方损失函数

每个数据点的 HMSE 最终应用

![](img/b87e989e58329680c8f0fc8029584260.png)

一阶导数是 w.r.t 'C '是

![](img/00a124ad95cbff63405d7bc02939c897.png)

现在让我们算出偏导数:

![](img/bbc51b0d190c2d3b4e66d414814cbe28.png)![](img/941d022c86b260d8cd3bde3f2002e348.png)

## 应用不同的损失函数

如果您决定在上述努力中应用不同的损失函数，我们可以尝试 Log-Cosh 函数，它也支持一阶和二阶导数。如果你应用 MAE 或 RMSE，两者都产生一个常数，因此从学习和收敛的角度来看，在神经网络梯度下降过程中是有益的！

![](img/8a9e9f91612de3e67d6d1a794ef0df00.png)![](img/7081a2053359d37cefbc72abfc887a71.png)

二阶导数是简单地将上述项乘以 x

![](img/b9b9dfac3f690b1efe1e1398be93123a.png)

# 梯度下降变体

![](img/db588769d0a5ef42af5d0672a472bf87.png)

## 批量-普通梯度下降

如在之前的沉浸式示例中，有 12 个数据点，并且模型参数 m & C 仅在结束时更新，即，在针对 12 个数据点的整个记录集计算通过每个数据点的所有导数和损失值之后。本质上，这是普通的批处理 GD，其中模型参数仅在所有数据点计算完成后更新——处理所有数据点被视为一个时期。

## 小批量—梯度下降

在上面的例子中，在 12 个数据点中，我们可以先处理 4 个数据点并更新模型参数，然后是接下来的 4 个数据点来更新参数，依此类推，直到所有的数据点都用完为止。基本上，在每个小批量(在我们的例子中是 4 个数据点)被处理之后，模型参数被更新，因此在一个时期内，参数被更新 n 次，其中 n =总数据点/小批量数据点。

## 随机梯度下降法

通常，SGD 使用单个数据点计算梯度，但大多数 SGD 应用实际上使用几个样本的小批量。因此，在每个时期开始之前，所有数据点都被随机打乱，然后进行小批量处理。对于具有大量局部最大值/最小值的误差流形，SGD 工作得很好(与批量梯度下降相比，现在有[种高级方法](http://ruder.io/optimizing-gradient-descent/))。这样，使用减少数量的数据点计算的稍微更嘈杂的梯度倾向于将模型从局部最小值中拉出到希望更优化的区域中。单个数据点确实有噪声，而小批量数据往往会平均消除一点噪声。因此，在使用小批量时，加加速度会降低。当小批量可以避免一些不良的局部最小值，但足够大以包括全局最小值或性能更好的局部最小值，并且理想地引导我们更容易落入放置最佳最小值的更大和更深的吸引盆地时，可能可以达到良好的平衡。

SGD 类似于对选民的横截面进行抽样以获得预测，而不是进行实际的选举。与批处理相比，学习率是惊人的，假设我们的总数据点是一百万(1M ),如果小批量是 10K，那么我们得到的加速因子是 1M/1K = 1000。加速因子可能不准确，并包括统计波动，但足以引导成本函数逐步降低。SGD 的一个好处是计算速度更快，并且可以并行化。

当构建梯度下降算法时，可以设置最大历元计数(迭代计数)以及损失因子差，它们协同工作以达到收敛或停止无休止的处理，无论哪一个先发生。点击进一步探索这些变体[。](/gradient-descent-algorithm-and-its-variants-10f652806a3)

# 系综引导的来回-前馈&反向传播

[榜首](https://medium.com/p/c18adab31cbe#99222)

# 链式法则

在我们之前的梯度下降示例中，我们看到了一个简单的函数 y = mx + C。这可以想象为一个单节点激活函数，它简单地采用一个输入来提供一个输出，本质上是将输入缩放 m 并添加一个偏差 c。
现在让我们想象一组这样的激活函数相互连接，一个的输出是下一个的输入。这是一个简单的线性网络，可能只有很少的节点。在我们的例子中，我们将考虑如下所示的 4 节点线性网络。同样的想法也适用于此——我们需要找到正确的权重和偏差，以便优化整体函数的输出，使原始输出和“互连函数”输出之间的任何误差最小。
为了演示这个想法，请看下图——这是一个具有输入节点和输出节点的两层隐藏式神经网络。

![](img/927f861131655f737044fc7bdbe2f1e4.png)

每个节点都是与其相连的前一个节点的功能。如果我们要更改输入节点中的输入或权重值，这种更改将向下级联，因为每个节点都将更改它们接收的输入，并最终反映在输出中。因此，输出变化可能看起来很复杂，但直觉上每个节点都会放大级联变化。由于每个节点相互依赖并且具有函数依赖性的概念，我们可以用数学公式表示一个复合函数来表示该网络的行为:

![](img/b6b91d28c02ba7afc9004de5c8b89cf3.png)

将所有等式合并为一个等式:

![](img/a81f5535e30df9a10ee42616dfb28570.png)

由于中间节点不是单独工作的，并且依赖于来自前面节点的输入，如果我们想要了解 w1 的微小变化对输出的整体影响，那么我们必须对输出 w1 从最后一个节点到第一个节点依次应用导数。合成的复合导数将是:

![](img/f8c1552b2fcde151ee13f40ab2619d43.png)

让我们在这里暂停一下，看看如何利用链式法则的详细例子。

# 链式法则在起作用——用一个例子来理解

微分链规则是反向传播的基础，获得直观的理解对全面理解神经网络大有帮助。通过下面的例子，我们可以解释链式法则是如何工作的，并了解因素的变化如何导致最终产出的变化。在下面的图表中，我们有 3 个以线性方式连接的激活函数，基本上任何输入通过它们级联，以给出遵循所述规则的输出。很容易理解:

![](img/73b634e2a46a0b4c128ca258b0fee878.png)

*   i/p 表示整个线性网络的输入
*   任何 i/p 被 w1 加权并补充以偏置 b1，共同表示为 z1，被馈送到激活功能#1
*   该函数将任何输入缩小 1/8 倍，得到 h1 作为输出
*   相同的模式重复，直到输出 h3
*   最后，我们有一个误差函数，其中如果我们知道实际 h3 和预测 h3，就可以计算误差/成本，但现在我们忽略这部分

让我们列举从输出到输入的上述线性网络的方程

*   *h1 = f1(w1 * x+B1)
    =(w1 * x+B1)/8*
*   *H2 = F2(w2 * h1+B2)
    =(w2 * h1+B2)/7*
*   *O = H3 = F3(w3 * H2+B3)
    =(w3 * H2+B3)/9*

![](img/32082378541845646f016a06c76c6f48.png)

如上所示，基本上你在 x 轴上的任何摆动都会按照我们的例子缩小，然后由于每一层的重量和偏差而略微上升。还有一点需要注意的是,“h”不知道 x 发生了什么，只是改变了“g”的变化,“g”也不知道 x 的变化，只是摆动“f”等等。现在 x 的任何变化都会被 f 的变化率放大，然后是下一层等等。
O = h(g(f(x)))h w . r . t . x 的变化为

![](img/79bbd059c288314d5e6c150685636172.png)![](img/b8f02cb8263734f48f13ea66d62cff7f.png)

链式法则不仅仅是分母和分子的单位相消——它是一个波动的级联，在每一步都可以放大、缩小或调整。链式法则适用于任何数量的变量(f 取决于 g 取决于 h，依此类推)，只是级联摆动。把它想象成放大不同变量的视角——从 dx 开始向上看，你可以想象在波动到达 h 之前需要的整个调整链。

O w.r.t w1 的任何变化(w1 也是上述 x 的放大值)可以用链式法则写成，如下所示:

![](img/acf147b18c27f60db7481603509c0452.png)![](img/17758778167d5626601fa0e24dcb90d2.png)

以上表格用数字数据总结了链式法则背后的思想

1.  A 列:考虑这个线性网络的几个输入
2.  B 列:计算 h1
3.  列 C:计算 h2
4.  D 列:计算 h3 —最终输出
5.  E 列:根据 w1 的变化计算新的 h3—只需计算 h3 相对于 w1 的变化率，然后乘以 w1 的变化，最后将其加到 H3 上，即可得到新值
6.  重复的行通过合并新的 w1 值并进行所有端到端计算来计算 h1、h2 和 h3，从而得出 h3 —注意 E 列数据和 D 列标题“新 h3”下的数据(在修改的 w1 上)是相同的
7.  F 列:使用近似值计算导数，如公式所示:

![](img/ed0a856be3d43eb1cee2bf8bcb70e512.png)

这里 O 只不过是计算 h3
用近似法和链式法则计算的值与图示相同

# 反向传播——反向链规则

在我们之前的线性节点网络中，让我们添加一个名为成本函数的最终函数。这将获得最终输出(使用给定模型(我们的线性网络)计算的 y 值也称为预测值),并计算与给定原始输出(原始 y 值)的差异。由于这是另一个函数依赖关系，现在我们的成本也受到输入、权重和偏差的影响，因此是它们的函数。

![](img/134a387b02ae89e51f9b6b27209e3809.png)

现在让我们在这个网络的末端附加一个“成本函数”,如上所示，很明显这个函数的输出也依赖于输入和中间权重。因此，我们也可以将相同的导数公式扩展到我们的成本函数:

![](img/7b8f585d08bcf35abdcfb700f9af809c.png)

在“通过示例理解链式法则”一节中，我们能够使用近似法找到复合导数。即通过将 w1 改变一个小值并计算新的输出，因此。

![](img/be7a7d35a85130ab0ba74303f54a3d75.png)

价值。
现在会出现一个问题，如何应用近似原理来计算真实神经网络中成本 w.r.t .权重的变化。走这条路是可行的，但是会导致计算速度变慢。让我们假设一个大的权重网络，为了找到成本 w.r.t w1 的变化，我们需要找到所有权重承载节点处的 C 和 C(具有δw1 ),对它们求和，得到它们的最终数量，然后应用近似公式。如果节点数以百万计，近似算法会嘎然而止，而链规则方法在将导数传播回网络时会很方便，通过梯度下降快速找到权重，以降低总成本，如下所示。

![](img/96f7849e90aa6f52701343742060dc97.png)

# 神经网络

## 网络

是时候深入研究真正的神经网络了，根据目前的理解，算出方程式，并将其应用到 python 代码中。符号和代码是基于由[迈克尔尼尔森](http://neuralnetworksanddeeplearning.com/chap1.html)的开创性的书。我不得不花相当多的时间来理解 python 代码中的符号、等式和推论。我在这里所做的是用更好的可视化来进一步简化它，这样它就可以很快被吸收，并且这本书可以被用作参考资源。

![](img/1d4ae496f19cc3cb003f18be49f42541.png)

想象一个 4 层的网络(如上所示):

1.  第 0 层—3 个节点的输入层
    输入没有转换，它们只是被传递
2.  第 1 层——包括 4 个神经元
    对于该层中的每个神经元，第 0 层输入被加权，最后添加一个偏置并馈入激活函数
3.  第 2 层——包括 3 个神经元
    对于该层中的每个神经元，第 1 层输入被加权，最后添加一个偏置并馈入激活函数
4.  第 3 层——包括 2 个神经元
    。对于该层中的每个神经元，第 2 层输入被加权，最后添加一个偏置并馈入激活函数

让我们给我们现在所说的赋予适当的符号，并用数学方法恰当地表达出来，这很容易理解。考虑该网络的输入用例也是很好的，但不需要完全匹配输入和输出，而是提供网络将如何处理整体数据的上下文和直观理解。
[MNIST](http://yann.lecun.com/exdb/mnist/) 是深度学习的标准火炬手数据集——它包含 60K 张手写数字的图像和每张图像的注释正确数值。

1.  输入是一个 28×28 像素的图像
    转换成一个 784 个输入的阵列，存储 0 到 1 之间的灰度值
2.  输出表示 0–9 之间的数字
    转换为 10 个输出的数组，每个输出为 0 到 1 之间的值，大于 0.5 的值表示该数字按顺序排列。在某种程度上，输出也可以被认为是该数字出现在 i/p 图像中的概率

## 数学表达的网络

一个完整的网络和完整的符号在这里给出，并得到一个完整的景观点击图片。

[![](img/9be3b7b7ab8c890b231a58c4250cab65.png)](https://avantlive.files.wordpress.com/2019/04/neural-net-eq-1.jpg)

## 基本定义

现在，让我们一步一步地定义所有的基本要素——输入、权重、偏差，请参考下图

*   **输入(在第一层)
    输入= x**
    通常是原始的或归一化的数字数据，在这一层中用 x 表示。还要注意，在这一层中，没有激活、权重和偏差，因此所有这些都为零，我们也可以说在这一层中:

![](img/11f5bc6878e7a30c66a1f91b4b4292cd.png)

我们随后会看到 z 和 a 是什么

*   **行和层(列)** Rows = **j** 和/或**k** Layers =**L**或**L**
    ***j***始终与当前层关联， ***k*** 是指第 **(l-1)层**。**L**’表示最后一层或一层的集合。
    还要注意的是，在上图中，神经元并没有从顶部等距排列，而是很好地放置在相应的行和层中，以匹配我们稍后将看到的矩阵表示。
*   **重量**

![](img/2fb6f8161dc385e4c9619be04d131fb7.png)

每个神经元从前一层神经元的输出中获得大量输入，然后将偏差合并为输入。j 和 k 符号和以前一样，如下图所示

![](img/ce511ed793281f17f86b374ef18666bc.png)

*   **偏置**

![](img/7455bb234b77163e6abab7e63dcb2728.png)

来自前一层的所有加权输入被相加并加到 j 行中 l 层节点的偏置，被馈送到 l 层和 j 行的神经元。

## 其他定义

现在让我们一步一步地定义下一个层次——组合输入、激活、输出、成本函数，请参考下图。

![](img/11f8e20e9732f13411b67c32e94a2b8d.png)

*   **神经元的输入**

![](img/1550c93c79573781db763be3e863596c.png)

*   **激活**

![](img/5425ece87c86860a7c276aebd7da44bd.png)

*   **成本**

![](img/676bea021ac806b3a67b8cd1cc2d4546.png)![](img/149b49886cae81327fe5641d663b2cd2.png)

*   从 MNIST 数据集的角度来看，输入的数量:50k 个训练数字图像，每个都单独表示为 784×1 的实数矩阵，该矩阵在 0 到 1 之间，是像素的灰度值

![](img/feb99206cac084253dcfa5fbcadfeac0.png)

*   从 MNIST 数据集的角度来看，输出:经过我们的神经网络后，是数字输出-10 的数组-代表 0 到 9 之间的每个数字-其值也在 0 到 1 之间，这是特定数字的概率值
    输出数量(对于给定的图像输入)= 10 个输出

![](img/86033502b0c09aca6451f97f81646e00.png)

*   从 MNIST 数据集的角度来看，原始输出:给定图像的经过注释和验证的数值-我们可以将其转换为 10 个值的数组，每个值表示数字 0 到 9，其中对应的数字为 1，其余的数字为零
    原始输出的数量(对于给定的图像输入-表示为每个数字为 10–1 的数组)= 10 个输出

![](img/84e9a696fb54c13eb1f36f973c4323d2.png)

*   从 MNIST 数据集的角度来看，输入/样本计数:50K 个训练样本

由于成本是输出激活的函数，我们可以写为:

![](img/33a27ec3771d99b06d2d63efcf09ec1d.png)

# 反向投影方程推导

![](img/64391a6fe97668ace8b2f295c5a964a2.png)

以链式法则为例，我们可以说，重量/偏差的任何波动都会影响组合输入

![](img/ebfcdc7b09f88ebaf7855e8c1c24dfcd.png)

这反过来影响产量

![](img/cd82c080ab4939bc6b2aa7a6b78a9253.png)

最后影响成本/误差

![](img/a8ad35ac2dd314cf03f6ca69435e738e.png)

作为推论，输入的任何变化都会影响输出和成本，输出的任何变化也会影响成本，不管重量/偏差的变化，也就是说，每个中间组件都会影响它的邻居和通道中的所有其他组件。相反，最终成本的任何变化都依产出、投入、权重和偏差的顺序而定。将 w.r.t .枚举到第 l *层节点 j 中的上述符号:*

## 变化和影响的可能组合

![](img/5753834a6aa3bfae287e3580031a832a.png)![](img/1a0f14e11c18e693bcac7db5306988cb.png)![](img/adadbb3a0bcd49218748d2bed4c2a0db.png)

当发现成本的变化时，权重/偏差的变化产生 4 个重要的等式，包括 ***反向投影*** 算法— BP1…BP4。

![](img/e1c68be431346f3da12e9f4325361e75.png)

## 成本与重量的变化

参照上图，让我们来算出第一个也是最重要的等式——成本变化与重量变化的关系

![](img/8993c5db63cef8efe1bc28e62c2b0c25.png)

## 成本相对误差的变化

![](img/a7e66997241626564e401cb86a6ff017.png)

## 最后一层输入的成本变化

![](img/87e26c16a513f0c16eb5f3026e9bf207.png)![](img/e9d15217a3c30e40b068ec71f9307c77.png)

## 中间层输入的成本变化

我们可以使用全导数，但这很繁琐，我们将看到如何通过在单线多层网络上应用链式法则来推导，并将其用于多行多层网络，理解其背后的直觉，但现在等式如下:

*   向量形式:

![](img/a6340a273a35c36d9f582f6f40cf0f6a.png)

*   基于网络中的每一行:

![](img/6d6c411c1c43b7d981864b963cc2b4b7.png)

## BP2 —直观推导—单行网络

下面让我们考虑一个线性网络，它有四个神经元，每个神经元都有权重、偏差、输入/激活和输出，如图所示。上标代表它们所在的层。

![](img/1c1007d2d7ad8e4b087eafa0d2b28a45.png)![](img/9c5c111e6bdee7422a1b6170d5542a39.png)

**向前传递:激活**

![](img/4e4f6f540c17ef11dcd45cb03e6d3413.png)![](img/8ebd59b45d82983dadf772aa17612263.png)

**反向传递:优化重量以降低成本**

根据梯度下降和链式法则，我们知道我们需要计算导数，从而计算“w”和“b”中的变化，以使成本最小，即——回想一下，w 中的任何波动都会影响通道中的所有中介，我们最初尝试找到最后一层的成本变化。对于单排神经元多层网络，更容易计算中间值。按链规则:

![](img/879ef7d98440ac2424399599fd1fc0de.png)![](img/e7912595bfc046f5da870011a0661888.png)

现在，我们可以总结重量的“反向传递”,类似地，您也可以测试偏差(鼓励读者进行详细的测试，为了简洁起见，省略了测试),如下所示:

![](img/15c0c56824c090012c910e84db143403.png)

## BP2 —直观推导— 2 排 4 层网络

![](img/8968f23cdd6adf5115359381400fe879.png)

让我们关注第 4 层，根据我们之前的理解，我们可以计算出如下激活:

![](img/1a21fd1b96b3be8de1f70fe42aee0f88.png)

计算从第 4 层到第 3 层的反向通路，总结如下:

![](img/634ab3fbf284b3c65d23e3cb5f1dab5e.png)

## 反向投影—一种不同的拍摄方式

![](img/ac23181a445dbdcbf7c25efa7acb274d.png)

如上图所示，**激活 w.r.t 第 3 层(从 3 到 4):** 只不过是第 4 层权重乘以第 3 层输出并加到第 4 层偏置上的和，反馈给激活函数，给出第 4 层的输出，即

![](img/9f9aab0b53a8bde4eb04b189f348cfca.png)

而**反向传播 w.r.t 第 3 层(从 4 到 3):** 是第 4 层权重转置乘以第 4 层成本变化 w.r.t 输出第 3 层激活差异的 hadmard 乘积。下图对此进行了说明。

![](img/55f5d479f3748e5bd834251d1bb0df19.png)

# 裸神经网络的内部工作——与代码匹配的矩阵

[顶端](https://medium.com/p/c18adab31cbe#99222)

## 我们神经网络上的 MNIST 数据集—节点和层

类似于“hello world”程序对任何语言都是事实，MNIST 数据集是神经网络学习的事实。它包含 60K 训练图像和 10K 测试图像。这些图像被标准化以适合 28×28 像素的分辨率，并进行抗锯齿处理以给出灰度。我们将继续构建一个神经网络，其:

![](img/601ef46f4fc65767904b1793d010d5c0.png)

Generated with NN-SVG Tool

1.  第一层——输入层:
    将是一个 784 节点——以线性 784×1 阵列矩阵的 28×28 像素边界框图像为特征
2.  第二层—隐藏层

![](img/8a4ee69fb71d9136ac59f93fd1312da1.png)

3.第三层—隐藏层
将是 40 个节点的隐藏层—权重矩阵将是(40×100)，偏差矩阵将是(40×1)

4.第四/最后一层—输出层
将是 10 个节点的输出(伪隐藏)层—权重矩阵将是(10×40)，偏差矩阵将是(10×1)。如此选择最后一层，使得每一层将代表一个数字(数字 0…9 中的任一个。因为该值是实数，所以输出表示该特定数值的概率，比如说大于 0.5 是肯定的，小于 0.5 是不可能的。

我们将使用上述神经网络架构来理解迈克尔·尼尔森的书中给出的 python 代码。这在 python 中提供了一个紧凑、简单的最小神经网络[实现。](https://github.com/mnielsen/neural-networks-and-deep-learning)

1.  将下面的 repo 克隆/复制到本地目录
    [https://github . com/mnielsen/neural-networks-and-deep-learning . git](https://github.com/mnielsen/neural-networks-and-deep-learning.git)
2.  移动到您克隆的本地目录，并从这里启动 python 2.6 或 2.7
3.  运行以下代码片段开始:

# Python 中的整体 NeuralNet

查看 network.py 的源代码，并按照下面提到的函数进行操作，以便更好地理解 python 逻辑的功能！

1.  **SGD 函数**
    (循环遍历次数)
    a .参数:
    training_data —相应格式化的训练数据矩阵
    epochs —对整个数据集进行迭代的次数
    mini_batch_size —顾名思义
    eta —学习率乘数
    test_data —相应格式化的测试数据矩阵—用于评估学习到的权重和偏差
    b .混洗所有 50K 个训练记录(每个包含 784
2.  **update_mini_batch 函数**
    (循环每个小批量计数)其中小批量计数=总训练样本除以小批量大小
    a .将权重和偏差矩阵初始化为零
    a .执行反向传播(包括前馈和反向传播)。循环每个训练记录+其小批量输出记录
    c .获取增量矩阵并添加到之前的增量矩阵(针对权重和偏差)
    d .计算 GD 并从权重和偏差中减去
3.  **反向传播函数** a .执行前馈——围绕每层权重/偏差循环计算每层的输入&激活矩阵
    b .执行反向传递
    c .首先计算最后一层增量
    d .从倒数第二层循环到第一层&计算每层权重和偏差的增量矩阵

前馈和反向反馈-用 Python 计算的矩阵

![](img/1ba15c5ef9d41ac2bd0b043ab26de548.png)

**4。评估函数** a .使用 SGD 计算的权重和偏差，对训练输入
执行前馈 b .获取最终输出并将其与实际输出
c .报告比较的正确结果计数

*希望它对你的深度学习之旅有所帮助，如果你想联系，请给我发电子邮件*[](mailto:dataspring.avp@gmail.com)

# *学习曲线回溯—参考文献和致谢*

*[榜首](https://medium.com/p/c18adab31cbe#99222)*

*这些是我阅读、思考和吸收的书籍、博客和代码，因为我试图理解深度学习，并希望通过在这里陈述它，可能有助于在你的旅程中引用它们，同时感谢所有类似地帮助打造深度学习的人。*

***书籍***

1.  *[神经网络和深度学习书籍](http://neuralnetworksanddeeplearning.com/)*
2.  *[数据科学家实用统计](https://www.amazon.com/Practical-Statistics-Data-Scientists-Essential/dp/1491952962)*
3.  *[掌握特色工程](https://www.amazon.com/Feature-Engineering-Machine-Learning-Principles/dp/1491953241)*

***代码***

1.  *[简单的 GD 代码](https://www.bogotobogo.com/python/python_numpy_batch_gradient_descent_algorithm.php)*
2.  *[尼尔森书中的神经网络代码](https://avantlive.wordpress.com/#)*

***激活功能***

1.  *[深度学习的基础——激活函数](https://www.analyticsvidhya.com/blog/2017/10/fundamentals-deep-learning-activation-functions-when-to-use-them/)*
2.  *[立方体功能](/activation-functions-in-neural-networks-83ff7f46a6bd)*

***损失函数***

1.  *[所有机器学习者都应该知道的 5 个回归损失函数](https://heartbeat.fritz.ai/5-regression-loss-functions-all-machine-learners-should-know-4fb140e9d4b0)*
2.  *[原木损耗](http://wiki.fast.ai/index.php/Log_Loss)*
3.  *[神经网络中的损失函数](https://isaacchanghau.github.io/post/loss_functions/)*
4.  *[余弦相似性——理解数学](https://www.machinelearningplus.com/nlp/cosine-similarity/)*
5.  *[二元交叉熵](/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a)*
6.  *[交叉熵损失和 Softmax](https://deepnotes.io/softmax-crossentropy)*

***梯度下降***

1.  *[机器学习 101:梯度下降的直观介绍](/machine-learning-101-an-intuitive-introduction-to-gradient-descent-366b77b52645)*
2.  *[梯度下降:你需要知道的一切](https://hackernoon.com/gradient-descent-aynk-7cbe95a778da)*
3.  *[梯度下降——初学者指南](/gradient-descent-a-beginners-guide-fa0b5d0a1db8)*
4.  *[保持简单！如何理解梯度下降算法](https://www.kdnuggets.com/2017/04/simple-understand-gradient-descent-algorithm.html)*
5.  *[线性回归](https://eli.thegreenplace.net/2016/linear-regression/)*

***反向传播***

1.  *[神经网络和反向传播浅显易懂](https://medium.com/datathings/neural-networks-and-backpropagation-explained-in-a-simple-way-f540a3611f5e)*
2.  *[神经网络&反向传播算法，讲解](https://ayearofai.com/rohan-lenny-1-neural-networks-the-backpropagation-algorithm-explained-abf4609d4f9d)*
3.  *[我试图理解反向传播](http://www.cl.cam.ac.uk/~mjcg/plans/Backpropagation.pdf)*

**原载于 2019 年 4 月 29 日*[*http://avantlive.wordpress.com*](https://avantlive.wordpress.com/2019/04/29/fathoming-the-deep-in-deep-learning-a-practical-approach/)*。**