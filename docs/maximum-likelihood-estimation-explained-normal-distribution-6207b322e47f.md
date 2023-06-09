# 最大似然估计解释-正态分布

> 原文：<https://towardsdatascience.com/maximum-likelihood-estimation-explained-normal-distribution-6207b322e47f?source=collection_archive---------1----------------------->

## 维基百科对最大似然估计(MLE)的定义如下:

> 通过最大化似然函数来估计分布参数的一种方法，使得在假设的统计模型下观察到的数据是最可能的。

为了理解这个定义，让我们看一个简单的例子。假设我们有一些连续的数据，我们假设它是正态分布的。通过假设正态性，我们简单地假设我们的数据分布的形状符合流行的高斯钟形曲线。我们不知道的是曲线有多“粗”或“细”，或者峰值出现在 x 轴的什么位置。

![](img/d18e66cbc3bfe35fafb8d6242c9dca74.png)

We assumed the general Gaussian bell curve shape, but we have to infer the parameters which determine the location of the curve along the x-axis, as well as the “fatness” of the curve. Our data distribution could look like any of these curves. MLE tells us which curve has the highest likelihood of fitting our data.

这就是估计或推断参数的地方。从统计学上我们知道，我们的高斯分布的具体形状和位置分别来自于 **σ** 和 **μ** 。换句话说，μ和σ是我们感兴趣的参数。这两个参数定义了我们的曲线，正如我们看到的正态分布概率密度函数(PDF)一样:

![](img/fec9c10f29b75b9e50156f2773178aed.png)

# 我们如何使用 MLE？

仍然记住我们的正态分布示例，目标是确定我们数据的μ和σ，以便我们可以将我们的数据与其最有可能的*高斯钟形曲线*相匹配。用我们的语言来说，技术上是正确的，我们可以说，我们正在寻找一条曲线，在给定一组曲线参数的情况下，使我们的数据的概率最大化。换句话说，我们最大化数据的*概率，同时最大化曲线*的*可能性。也许后一种解释是更直观的思考问题的方式，但两者都是正确的，我们将使用第一种视角来处理问题。*

为了使用最大似然估计，我们必须做出两个重要的假设，它们通常一起被称为 *i.i.d.* 假设。这些假设表明:

1.  数据必须独立分布。
2.  数据必须完全相同地分布。

换句话说， *i.i.d.* 假设要求任何给定数据点的观察不依赖于任何其他数据点的观察(每个收集的数据点都是独立的实验)，并且每个数据点都是从具有相同参数的相同分布族中产生的。

## 数学

通常，参数μ和σ一起表示为一组参数θ，即:

![](img/711976107150aa4c41373159c7b9d42d.png)

我们可以将问题建立为条件概率问题，其目标是在给定θ的情况下最大化观察到我们的数据的概率。对于大小为 *n* 的数据集，从数学上来说，它看起来类似于:

![](img/ed676b6b04d7ab2c3cabcd55b930fca3.png)

然而，因为我们正在处理一个连续的概率分布，上述符号在技术上是不正确的，因为观察到任何一组连续变量的概率都等于零。从概念上讲，这是有意义的，因为我们可以在连续域中得出无限多的可能变量，并且将任何给定的观测值除以无穷大总会得到零概率，不管观测值是什么。

我们需要考虑概率密度而不是概率。不去探究两者之间区别的技术细节，我们将只陈述连续域中的概率密度类似于离散域中的概率。因此，在这个最大化问题中可以使用概率密度。为了纠正我们的符号，我们会说:

![](img/4e7c942c6aa50b09adbe43aa49f71cb3.png)

我们希望将观察数据的概率密度最大化为θ的函数。换句话说，我们希望找到μ和σ值，使得这个概率密度项尽可能高。我们习惯于将 *x* 作为约定俗成的自变量。但在这种情况下，我们实际上是把θ作为独立变量，我们可以把 x_1，x_2，… x_n 看作一个常数，因为这是我们观察到的数据，不能改变。

从概率论中，我们知道多个独立事件全部发生的概率称为*联合概率*。我们可以将每个数据点观察视为一个单一事件；因此，我们可以将我们的精确数据集的观察视为一系列事件，并且我们可以如下应用联合概率密度:

![](img/32739eea76b5f468af5d4aec0397f1c4.png)

记住，目标是通过找到最优θ来最大化这个概率密度项。为了用数学方法表示这一点，我们可以说，我们寻求这一项相对于θ的“argmax ”:

![](img/e99986ea62b1756d3c9bffa53c1012d9.png)

因为我们在寻找一个最大值，我们的微积分直觉应该告诉我们是时候对θ求导，并将这个导数项设置为零，以找到我们沿着θ轴的峰值位置。这样，我们可以将联合概率密度项的 argmax 等同于联合概率密度项对θ的导数等于零时的情形，如下所示:

![](img/e7f2507d28953a0840b5e577137e6325.png)

现在，唯一的问题是，这不是一个很容易计算或近似的导数。幸运的是，我们可以在这个场景中应用一个简单的数学技巧来简化我们的推导。实际上，我们可以使用单调函数来改变导数项，这将简化导数计算，而不会改变最终结果。单调函数是两个变量之间保持原始顺序的任何关系。单调函数要么总是增加，要么总是减少，因此，单调函数的导数永远不会改变符号。我们这里使用的单调函数是自然对数，它具有以下性质(不包括证明):

![](img/4f6d7d1b3aaf1f6b714ebd95c0b2b5d9.png)

所以我们现在可以把我们的问题写成如下。请注意，下面第三项和第四项之间的等式是一个性质，其证明没有明确显示。

![](img/5d3c1c4054a4ec823d453ecad53ed52c.png)

为什么可以使用这种自然对数的技巧？由于自然对数的单调递增性质，采用原始概率密度项的自然对数不会影响 argmax，这是我们在这里感兴趣的唯一度量。当然，它改变了我们的概率密度项的值，但它没有改变全局最大值相对于θ的位置。从数学上讲，我们可以把这个逻辑写成如下:

![](img/be398a95f556de63731b2d9e7d6de9ed.png)

为了进一步说明这一概念，这里有几个函数沿着它们的自然对数(虚线)标绘，以表明沿着 x 轴的最大值的位置对于该函数和该函数的自然对数是相同的，尽管最大值本身显著不同。

![](img/b5c88b9657960b78b2d833e6d3715ff2.png)

垂直的黑色虚线表示函数与其自然对数之间的最大值对齐。这些线绘制在 argmax 值上。如我们所述，这些值对于函数和函数的自然对数是相同的。这就是为什么我们可以在这个问题中使用我们的自然对数技巧。

回到现在的问题，我们有:

![](img/9a8bf577bda65180c25f965dac191c8a.png)

我们希望求解θ，以获得最佳参数，使我们的观察数据与高斯曲线最佳拟合。现在让我们考虑一下我们要推断的两个参数，μ和σ，而不是符号表示θ。我们将切换到梯度符号:

![](img/1103185a121ffd0ee3b740aa798eabc7.png)

让我们从求关于μ的梯度开始。我们将在这里用正态分布的 PDF 代替 *f* (x_i|μ，σ)来做这件事:

![](img/e68f35aeab810fa53a2adc0434eb5603.png)

使用这里没有证明的自然对数的属性，我们可以将其简化为:

![](img/0d23f8eee31ecc063dec1fefa31871d0.png)

此外，

![](img/950f01dd5ec6c07b45bfb8efabe2de67.png)

设最后一项等于零，我们得到μ的解如下:

![](img/5cb2ef84d3f9569c544bf7df96ef88f5.png)

我们可以看到，我们的最优μ与我们的最优σ无关。现在，我们将以类似的方式，通过对σ求梯度来求解σ:

![](img/ddc248434efcf21ef50318d445292ccf.png)

设最后一项等于零，我们得到σ的解如下:

![](img/7e2680c5af018785d3265c492a24f8b6.png)

现在我们有了。如果我们最近做过统计，我们的最佳μ和σ导数应该看起来很熟悉。这些参数计算出的公式与我们用于平均值和标准偏差计算的公式完全相同。这不仅仅是巧合。这是正态分布的一个性质，假设我们可以进行独立同分布假设，这个性质就成立。

但是在这里理解 MLE 的关键是将μ和σ *而不是*视为我们数据集的均值和标准差，而是将*而不是*视为最有可能拟合我们数据集的高斯曲线的参数。当我们将 MLE 应用于贝叶斯模型和分布时，这种思路将会派上用场，在贝叶斯模型和分布中，计算中心趋势和离差估计量不是那么直观。