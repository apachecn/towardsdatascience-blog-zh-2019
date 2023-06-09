# 困惑矩阵——深度探究

> 原文：<https://towardsdatascience.com/confusion-matrix-deep-dive-8a028b005a97?source=collection_archive---------11----------------------->

![](img/b9ae864caa391fb97e3c175d4fa356b6.png)

## 将机器学习指标转化为现实世界

解释如何计算机器学习指标的帖子有几百个，而且指标很多！为您的机器学习算法模型选择正确的指标进行优化是一个很大的挑战，我们通常没有正确的答案。我们是应该使用像 MSE 这样对异常值更敏感的度量标准，还是应该使用像 MAPE 这样对百分比更敏感的算法？因此，一个更重要的问题是，我们如何将这些不同的度量标准转化为业务团队更切实的东西？或者回答日常的问题，是否值得继续改进模型？如果模型的 AUC 提高 1%,我们会赚多少？在本帖中，我们将尝试回答这些问题。

通常在回归问题中，我们试图减小预测值(yhat)与实际值(y)之间的距离，并选择产生最小误差的变量的权重。在分类问题中，优化这种类型的度量是没有意义的，因为我们要么有一个二进制类，距离将总是 0 或 1。在多类问题中，我们将有更长的距离，但不会有更大的误差，因为这些类是相互独立的。我们如何解决这一僵局？

# 这一切都始于准确性。

第一步是统计点击次数。每当预测值等于实际值时(我们称预测值为 yhat，实际值为 y ),我们就认为是命中情况，精确度定义为:

![](img/adc9bc63e6c56fa6b38a9c5cd199e88a.png)

这是一个广泛使用且相当危险的指标。它隐藏了你的模型中的一些可能的缺陷，并可能导致你做出错误的决定。

让我们看一个欺诈分类的例子。我们有 100，000 条观察结果，其中 1%是欺诈案例。如果你的模型很差，你说所有的值都不是欺诈，你仍然有 99%的准确率，这看起来很好，但实际上你的模型完全没有用，因为它不能识别任何欺诈者。

# 混淆矩阵

为了解决这个问题，我们需要更完整的度量标准，让我们不仅知道有多少命中，而且知道模型有多敏感。

为此，我们将绘制著名的混乱矩阵。这是一个矩阵，我们将实际值放在列中，将预测值放在行中。因此，行和列的交集成为我们的度量。(倒版的并不少见)

![](img/94acc8ed2e209fae857a2a2aea55b296.png)

我们现在可以在混淆矩阵中看到，有两种类型的命中和两种类型的错误，现在让我们来关注它们。就准确性而言，没有差异，只有命中和未命中。现在我们开始区分它们。

在命中中，我们可以有 T **真阳性(TP)** (即类别为 1，为欺诈，算法识别为 1，欺诈)。以及**真阴性(TN)** (为 0，模型预测为 0)。

至于错误，我们也有两种类型，**假阳性(FP)** (当它不是欺诈时，模型预测为欺诈)，和**假阴性(FN)** ，当它实际上是欺诈时，模型预测为非欺诈。

![](img/5d5d091c81f6a2d871baee7f4c920503.png)

在统计学中，我们称假阳性**为 I 型错误**。它是测试的**显著性水平**，用α (alpha)表示。一个非常常见的水平是著名的 5%,它的解释是，在α倍(如 5%)我们将拒绝零假设(H0)时，它是真实的。

**第二类错误**，我们的假阴性，不太受欢迎，一个原因是它不能直接选择(就像我们选择显著性水平一样)，在统计学上它代表了检验的**功效，以及变化的形式。它使用不同的模型或增加样本量。它由希腊字母β (Beta)表示。当零假设为假，但我们错误地未被拒绝时，第二类错误发生。**

这些定义可能会令人困惑，因为它们是相对于我们选择的类别 1 和 0 而言的。一个简单的规则是将最感兴趣的等级设为 1，通常最感兴趣的是它变得更贵的时候。

# 精确度或灵敏度/召回率

![](img/cd29e5c739012b86858018db1e54cacb.png)

从混淆矩阵中，我们可以建立至少十几个指标，但有两个更重要，精度和召回率。第一个告诉我们所有我们认为是 1 级的案例(在我们的例子中，所有预测为欺诈的案例)中有多少是正确的(即，有多少是真正的欺诈)。他告诉我们，回忆给了我们敏感性的概念，在目标为 1 的所有可能案例中，我们可以捕捉多少，在我们的例子中，在所有可能的欺诈案例中，我们的模型可以识别多少。请注意，这两个指标的分子相同，但分母不同。

在我们最初的例子中，我们有 99%的准确率，我们的敏感度为 0%，因为我们没有发现任何欺诈案例。

![](img/34767f41bcb9b7a2c126eee339964596.png)

# 更准确还是更灵敏？如何选择

就像机器学习中的几乎所有事情一样，我们在这里也有一个很大的权衡，我们不能同时拥有一个准确和敏感的模型，或者我们改善一个指标或改善另一个指标。让我们更深刻地理解这一点。

假设你需要训练一个模型来预测谁会得癌症(y = 1)。让我们了解一下每种可能性会发生什么:

*   **TP** : (y = yhat = 1) →我们已经正确识别出谁会得癌症，这样这个人就可以得到治疗，增加生存的机会。
*   **TN** : (y = yhat = 0) →我们正确识别谁不会得癌症，这样一个人就可以安心回家，不用担心治疗。
*   **FP** : (y = 0 & yhat = 1) →这里问题开始了。
    我们预测这个人会得癌症，而他不会得。所以她将不得不在不必要的考试上花费时间和金钱。但它会活下来。
*   **FN** : (y = 1 & yhat = 0) →也许这是主要问题，这个人会得癌症，而我们的模型预测不会，所以她会高高兴兴回家，不会被检测，大大增加她的生命威胁。

因此，我们通过使模型更精确来减少 I 型误差，或者通过使模型更敏感来减少 II 型误差，在这种情况下，哪种选择是正确的？好吧，如果让我来选择预测自己健康状况的模型，我会让模型尽可能的灵敏，即使这会导致精度降低。但是立法者不这么认为，因为第一类错误也是昂贵的。那么如何选择呢？

# 阈值

假设模型不直接预测类别，而是计算每个观察值属于该类别的概率，如果该概率大于 50%，则认为该观察值属于类别 1，否则，属于类别 0(或任何数目的类别)，这称为阈值，
，它是将类别分开的截点。我们现在要开始做的是想一个选择这个切口的策略。

因此，阅读混淆矩阵的另一种方法是理解类别 0 和类别 1 的概率分布，如图所示:

![](img/83fcb80bd448fc128aed6f423426d8e3.png)

Moving the cut from 50% to 75% makes the model more accurate and less sensitive.

如果我们想要一个超级准确的模型，我们将阈值从 50%更改为 75%，因此只有当我们对预测非常确定时，我们才会预测为真，相反，如果我们需要一个非常敏感的模型，只需更改它一点点的准确性，我们将阈值降低到，例如，
25%，我们将预测更多的情况为真。

![](img/0a7f46dba87d255581b0203ffa527ebb.png)

Moving the cut from 50% to 25% makes the model much more sensitive but less accurate.

# 用财务矩阵优化阈值

如果混淆矩阵取决于使用的阈值，选择哪一个？把赔率变成职业的最佳切入点是什么？让我们使用下面的技术。让我们创建一个混淆矩阵，但我们不是输入预测数量，而是输入击中和未击中的单位成本。下面举个例子:

![](img/c3d0d20a36aad6a488810a1c62774ac6.png)

**TP**:1000 万融资的 1%利润
**FP** :我担心如果我们的模型没有识别出欺诈者:-1000 万。
**FN** :如果我们说某个客户是欺诈，而事实并非如此，我们就不再赚取利润。
**TN** :正确识别的欺诈不欺诈我们。

之后，我们将把我们的财务混乱矩阵乘以模型得出的混乱矩阵。你的结果将是我们模型的盈利/亏损。之后，我们将测试不同的阈值，选择利润最高的阈值。机器学习模型不能考虑这一点，因为它的错误具有对称的成本，在现实生活中，我们很少对类型 I 错误和类型 II 错误具有相同的成本，每当成本不同时，我们需要选择正确的阈值。

![](img/7eee4b602a6c3d039b5b9a63ad60884f.png)

下面的代码迭代不同的切割，以确定哪个切割产生的利润最大:

![](img/d35ff02c7bec85e3553ad91a6c6623d3.png)

最后是我们的利润 x 削减曲线:

![](img/e728ddc7deda7f18b0f8b73243d5954d.png)

现在很容易决定削减 0.86。高于 86%的几率将被视为欺诈，低于 86%的几率将被视为通过。根据目前的数据，我们似乎需要一个比敏感模型更准确的模型。

# f1-分数

不使用精确度或召回率的替代方法是使用两者的平均值。代表精确度和灵敏度之间平均值的指标是 F1 分。此指标的唯一细节是它不是简单的算术平均值(求和并除以 2)，因为对比率使用简单平均值不是好的做法。相反，我们使用调和平均值来使度量对比率不均衡敏感:

![](img/dc4b2e65fe73d14a3351da693a0fe760.png)

第二种形式是 F-Beta，我们可以通过 Beta 参数在精确度和召回率之间选择权重:

![](img/47503f6a84c05675d5ea73fc1e8d2907.png)![](img/95c0f274623a309519bdbcf16e4b8362.png)

Matriz de confusão expandida

# 后续步骤

一个不同的甚至比我们的混淆矩阵更强大的指标是所谓的 AUC，它修复了这里提出的指标的一些“缺陷”,可以在下面的帖子中检查:

[](https://medium.com/@marcos.silva0/deep-dive-auc-e1e8555d51d0) [## 深潜 AUC

### 将机器学习指标转化为现实世界

medium.com](https://medium.com/@marcos.silva0/deep-dive-auc-e1e8555d51d0) 

参见:

*   [数据科学](https://medium.com/swlh/data-science-and-the-data-scientist-db200aac4ea0) [的范围是什么；](https://medium.com/beacon-insight/ci%C3%AAncia-de-dados-e-o-cientista-de-dados-72634fcc1a4c)
*   [为数据科学家推荐书籍、课程和电影。](/how-to-become-a-data-scientist-2a02ed565336)
*   [解释机器学习；](/the-ultimate-guide-using-game-theory-to-interpret-machine-learning-c384cbb6929)
*   [统计学简史](http://a%20brief%20history%20of%20statistics/)；