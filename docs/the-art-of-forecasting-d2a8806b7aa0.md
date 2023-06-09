# 预测的艺术

> 原文：<https://towardsdatascience.com/the-art-of-forecasting-d2a8806b7aa0?source=collection_archive---------13----------------------->

![](img/3b093935e0c554fd8c9786f1ffc7e1dd.png)

Photo by [Emmanuel Holveck-Lafay](https://www.pexels.com/@dphot?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/close-up-photo-of-person-holding-lensball-2626979/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

## 当我们试图预测未来时，到底发生了什么

数据科学是许多学科的混合体——统计推断、分析、可视化、分类和预测。人们普遍认为最令人着迷的是预测。

预测未来听起来像是魔术，无论是提前发现潜在客户购买你产品的意图，还是计算出股票价格的走向。如果我们能够可靠地预测某事的未来，那么我们就拥有巨大的优势。

机器学习只是放大了这种神奇和神秘。随着预测模型复杂性的增加(以失去可解释性为代价)，它们能够发现以前未被注意到的相关性，并利用以前难以使用的数据。

但是从本质上来说，预测其实很简单。今天我们将介绍**一个思考预测的心智模型**，希望它能揭开这门艺术的神秘面纱，并鼓励你将预测添加到你的定量工具包中。

# 线性回归预测

我们在统计学中学习的第一个模型是线性回归。它是多用途的，可解释的，并且惊人的强大。这是一个很好的工具来说明预测是如何工作的。

对线性回归如何工作的非数学描述是，它试图通过代表数据的点尽可能最佳地拟合一条线。这条线试图捕捉你的数据的趋势。下图显示了这条最佳拟合线(蓝色)的样子。让我们来解开到底发生了什么:

1.  每个点代表一个观察。它的垂直位置是由点表示的观察的目标变量(我们试图预测的)的值。而点的水平位置就是我们的特征值(我们的自变量)。
2.  目标变量和我们的特征之间显然存在正相关关系——请注意圆点如何向右上方移动。
3.  最佳拟合线是沿着趋势方向，穿过尽可能多的点的线。这条线概括了我们的目标和我们的特征之间的关系。

![](img/6a3000a4e8e5dc6a9ecab707eed954c8.png)

The Line of Best Fit (In Blue)

那么这和预测未来有什么关系呢？让我们想象一下，我们正试图预测美国的 GDP(经济)增长。我们假设 GDP 增长和企业利润率(企业盈利能力如何)之间存在关系。我们将它们绘制成图，并看到以下关系(**所有数据都是我编造的，仅用于说明目的**):

![](img/8e431f1376e98373fc0c8201cbbfeaba.png)

GDP Growth vs. Profit Margins (Fake Data)

强正相关！那么企业利润率高是否预示着 GDP 的高增长？别急，这是你脑中的声音应该在低语的地方:

> "相关性并不意味着因果关系."
> 
> —你脑海中的声音

诚然，经济扩张时期通常伴随着丰厚的企业利润(和丰厚的利润率)。但我们正试图了解利润率是否能预测经济增长。为此，我们需要修改我们的分析:

*   **错:**当期利润率对比当期 GDP 增速。
*   **正确:**当前利润率对比**明年的** GDP 增长。

这种区别是关键。我们并不试图寻找与 GDP 增长同时相关的特征。相反，我们希望找到预测未来 GDP 增长的特征。也就是说，我们希望找到与下一期 GDP 增长相关的特征(我们的目标是下一年 GDP 增长的变化)。考虑到这一点，让我们重做散点图:

![](img/3ef4b1b0e74ae6790656873119a65d57.png)

Future GDP Growth vs. Current Profit Margins

我们的正相关去哪了？预测未来很难。当我们将一个变量切换到它的未来状态(并测量预测相关性)时，变量之间的强并发相关性通常会消失。

这并不意味着所有的希望都破灭了。通常，如果我们足够努力地寻找并创造性地思考，我们仍然可以找到一些真正具有预测性的关系。但不要指望这些关系会很强——根据我的经验(试图预测金融市场的未来)，0.20-0.30 的预测相关性已经很好了。

# 理解预测的心理模型

假设我们继续努力测试未来 GDP 增长的特征，并最终发现以下关系:

![](img/e2a9a058322be8fee1bf1e0e9f9ac8c6.png)

Future GDP Growth vs. Current Growth in Working Young

我们发现了未来 GDP 增长和目前观察到的年轻劳动者(25-35 岁)增长之间的关系。它不像我们之前看到的并发关系(GDP 增长和利润率)那样强有力，但这是一种预测关系，我们可以用它来建立预测模型(再次强调，这是我为了说明预测如何工作而编造的所有数据)。

那么我们如何建立模型呢？实际上已经完成了— **最佳匹配的蓝线是我们的型号**。我们通过简单地观察工作的年轻人口的当前变化来做出我们的预测(假设它是由金色虚线表示的值)。然后，我们沿着 y 轴(纵轴)查看黄金虚线与最佳拟合蓝线(绿色虚线)相交的值，该值就是我们的预测值。

![](img/1131ac25ca3a58d8cdfe7f71d7d9387e.png)

Making Our Prediction

好的，酷，这很简单。对于更多的功能，甚至是更复杂的预测算法，这个过程都是一样的。

但在更基本的层面上，我们的预测到底意味着什么？每一个预测，不管产生它的模型有多复杂，都可以被认为是一个条件预期。条件期望只不过是期望值的一种类型，也称为平均值。

那么，我是不是在告诉你，你那奇特的 XGBoost 回归器所产生的值只不过是一个平均值，确切地说，是你在初级统计课上学到的第一个概念？

差不多(有一些警告)。不相信我？让我们做一个思维练习。如果我让你预测明天的天气(不查互联网)，你会怎么做？你可以这样做，“昨天很热，现在是八月，我们在圣何塞，所以我预测明天会是晴朗炎热的。”

你为什么得出那个结论？这是因为，也许你没有意识到，你对你记忆中在圣何塞的所有日子做了一个心理盘点，那是夏天，前几天天气很热。在你脑海中相关的每一天的平均天气都是晴朗炎热的。

**所以你通过过滤相关的观察数据**(圣荷西的夏天，之前天气炎热)**并取这些观察数据的平均值来做出你的预测。**这就是我们作为人通常是如何直觉地做出预测的——那么我们为什么要期待模型和机器会有什么不同呢？答案是他们没有什么不同，除了他们可以处理更多的数据，并且以一种更少偏见的方式这样做。

**因此，为了理解预测未来是如何工作的，我的建议是，把每个预测看作是从最相关的先前观察到的观察值的平均值中得出的。**对未来的预测只是在回答以下问题:

> 当我看到类似的事情在过去发生时，接下来通常会发生什么？

# 可视化条件平均值(也就是我们的预测)

让我们用前面的例子来形象地说明我们所说的预测是条件平均值是什么意思。下图显示了我如何将线性回归可视化，以及更一般地，预测模型的输出。每个金色矩形是样本(我们的观察)的一部分，条件是特征变量在某些值之间。例如，左边的第一个黄金矩形可能只是那些对 GDP 增长(我们的目标，在 Y 轴上)的观察，其中年轻工作人口的增长率(我们的特征，在 X 轴上)在 0%和 0.1%之间。

![](img/2e6fca28650d49af30b631b826509bbc.png)

A Regression is Like a Bunch of Snapshots

注意蓝色预测线(最佳拟合线)是如何落在每个黄金矩形的中间的？这是设计使然——每个矩形的中间是该特定切片的平均值(回想一下，每个矩形代表一个切片)。随着我们获取越来越小的切片(随着我们增加矩形的数量，同时减少每个矩形的宽度)，条件平均值系列(由每个矩形的中间表示)收敛到回归线。

“但是等一下！”你在思考。其中一些矩形的中间显然不是该切片内观察值的平均值。例如，第一个黄金矩形只包括一个观察值，它在我们的预测线之上。所以我怎么能说预测线是条件平均值，也就是该切片内的平均值呢？

对于简单的线性回归，条件平均值与每个切片中观察值的平均值不匹配，因为回归算法在目标和要素之间建立了线性关系。但是并没有失去一切！我们的心理模型仍然有效。

OLS ( [普通最小二乘法](https://en.wikipedia.org/wiki/Ordinary_least_squares))，线性回归用来寻找最佳拟合线的方法，就像取一组条件平均值，但有一点扭曲。我们可以用投票类比来理解我的意思:

*   想象每个黄金矩形是一个独立的选区。
*   每个区域都希望将区域内蓝色预测线的值(与每个黄金矩形的垂直中点相同)设置为尽可能接近本地区域平均值(区域中所有黑点的 Y 轴平均值)。
*   当单个分区移动预测线时，该移动会影响所有分区中预测线的值(因为它必须保持为直线)。
*   每个分区影响预测线的能力与该分区内的观测数量成正比(观测越多，影响越大)。

**最终结果是，每个选区都尽最大努力将这条线拉向自己的平均值。与此同时，每个选区都感受到并受到其他选区**的每一次推拉，尤其是那些有大量观察数据的选区。最终，预测线以如下方式确定:

1.  每个选区都很满意，向自己选区的平均值移动了线，即使只是一点点。
2.  考虑了群体的整体平均值(因为每个人都试图将预测线移向自己的个人平均值)。

**因此，虽然线性回归做出的预测在严格意义上不是条件平均值，但由于每个选区将预测线拉向自己的平均值的方式，它与条件平均值相似。**

# 那又怎样？

条件平均值如何帮助我们更好地理解预测？嗯，它们是每个预测的基础支柱。不管有多复杂，每种算法在其最基本的层面上都试图识别本质上与它试图预测的观测相似的观测。并且它做出的预测是目标在那些最相似的观察值中的平均值的导数。

甚至有某些算法，如[k-最近邻](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)或仅使用非有序分类特征的线性回归，可以通过条件平均值进行显式预测。

因此，预测没有什么神奇的——无论是算法还是人类都无法将当前数据转化为对未来的精确预测。相反，我们都只是把过去发生的事情作为未来可能发生的事情的粗略指南。

# 关键要点

在构建预测算法时，我们应该记住两件事。**首先，因为我们用过去来预测未来，所以背景很关键。如果我们所处的环境与训练我们模型的可用历史有很大不同，那么我们就不能期望我们的预测表现良好。**

第二，这个心智模型对于思考过度拟合是有用的。我们可以通过遵循以下两个原则来构建一个能够合理概括的模型:

1.  确保每个条件平均值包含足够多的观察值(少量观察值的平均值比大量观察值的平均值更有可能出错)。我们可以通过不包含太多的特征来确保这一点——太多的特征(相对于观测值的数量)将导致非常精细的切片，每个切片只有非常少的观测值。
2.  **小心那些允许单个分区(切片)对其自己的分区内预测产生太大影响的算法。**包含过多非线性的算法(如多项式回归或深度神经网络)将允许每个分区将分区内预测拉至等于其分区平均值。这可能导致不合理的不稳定预测，不能很好地概括。

希望这是有帮助的！干杯！

***更多数据科学与分析相关帖子由我:***

[*数据科学家是做什么的？*](/what-do-data-scientists-do-13526f678129)

[*数据科学家面临自动化的风险*](/is-the-data-science-profession-at-risk-of-automation-ae162b5f052f)

[*拿到了数据科学的工作？*](/got-data-science-jobs-552e39d48da2)

[*了解 PCA*](/understanding-pca-fae3e243731d?source=post_page---------------------------)

[*了解随机森林*](/understanding-random-forest-58381e0602d2?source=post_page---------------------------)

[*理解神经网络*](/understanding-neural-networks-19020b758230?source=post_page---------------------------)