# 用决策树进行分类和回归分析

> 原文：<https://towardsdatascience.com/https-medium-com-lorrli-classification-and-regression-analysis-with-decision-trees-c43cdbc58054?source=collection_archive---------1----------------------->

## 通过理解决策树背后的基本概念和数学，学习构建分类和回归决策树！

**决策树**是一种受监督的机器学习模型，用于通过从特征中学习决策规则来预测目标。顾名思义，我们可以把这个模型看作是通过提出一系列问题来做出决定，从而分解我们的数据。

让我们考虑下面的例子，其中我们使用决策树来决定某一天的活动:

![](img/9e685e71632ed6a80df330164f9b6883.png)

基于我们训练集中的特征，决策树模型学习一系列问题来推断样本的类别标签。正如我们所见，如果我们关心可解释性，决策树是有吸引力的模型。

虽然上图说明了基于分类目标的决策树的概念(**分类**)，但是如果我们的目标是实数(**回归**)，同样的概念也适用。

在本教程中，我们将讨论如何用 Python 的`scikit-learn`库构建决策树模型。我们将涵盖:

*   决策树的基本概念
*   决策树学习算法背后的数学原理
*   信息增益和杂质测量
*   分类树
*   回归树

我们开始吧！

> 本教程改编自 Next Tech 的 **Python 机器学习**系列，带你从 0 到 100 的机器学习和深度学习算法。它包括一个浏览器内沙盒环境，预装了所有必要的软件和库，以及使用公共数据集的项目。这里可以开始[！](https://c.next.tech/2E7k6Dy)

# 决策树的基础

决策树是通过**递归划分**构建的——从根节点(称为第一个**父节点**)开始，每个节点可以拆分成左右**子节点**。然后，这些节点可以被进一步拆分，并且它们自己成为其结果子节点的父节点。

例如，看上面的图片，根节点是`Work to do?`，并根据是否有工作要做而分成子节点`Stay in`和`Outlook`。`Outlook`节点进一步分成三个子节点。

那么，我们如何知道每个节点的最佳分裂点是什么呢？

从根开始，数据在导致最大**信息增益** ( **IG** )的特征上被分割(下面更详细地解释)。在迭代过程中，我们然后在每个**子节点**处重复该分裂过程，直到叶子是纯的——即，每个节点处的样本都属于同一类。

在实践中，这会导致树非常深，有很多节点，这很容易导致过度拟合。因此，我们通常希望**通过设置树的最大深度来修剪**树。

# 最大化信息增益

为了在最具信息性的特征处分割节点，我们需要定义一个目标函数，我们希望通过树学习算法来优化该目标函数。这里，我们的目标函数是最大化每次分裂的信息增益，我们定义如下:

![](img/1cb6543fcba5bf02e6fdfc6489ba1e4f.png)

这里， *f* 是执行拆分的特征， *Dp* ， *Dleft* 和 *Dright* 是父节点和子节点的数据集， *I* 是**杂质度量**， *Np* 是父节点的样本总数， *Nleft* 和 *Nright* 是

我们将在下面的例子中更详细地讨论分类和回归决策树的杂质度量。但就目前而言，只要明白信息增益简单来说就是父节点杂质和子节点杂质之和的差——子节点杂质越低，信息增益越大。

注意，上面的等式是针对二元决策树的——每个父节点只被分成两个子节点。如果你有一个有多个节点的决策树，你可以简单地将所有节点的杂质相加。

# 分类树

我们先来说说分类决策树(又称**分类树**)。对于这个例子，我们将使用机器学习领域的经典产品 [*Iris*](https://archive.ics.uci.edu/ml/datasets/iris) 数据集。它包含了来自三个不同物种 *Setosa* 、 *Versicolor* 和 *Virginica* 的 150 朵*鸢尾*花的尺寸。这些将是我们的**目标**。我们的目标是预测一朵鸢尾花属于哪一类。以厘米为单位的花瓣长度和宽度存储为列，我们也称之为数据集的**特征**。

让我们首先导入数据集，并将特征指定为`X`，将目标指定为`y`:

使用`scikit-learn`，我们现在将训练一个最大深度为 4 的决策树。代码如下:

注意，我们将`criterion`设置为“**熵**”。这一标准被称为杂质测量(在前一节中提到)。在分类中，熵是最常见的杂质测量或分裂标准。其定义如下:

![](img/97306efc66fcea72f5f8996ccfa34920.png)

这里， *p(i|t)* 是属于特定节点 *t* 的类别 *c* 的样本的比例。因此，如果一个节点上的所有样本都属于同一个类别，则熵为 0，如果我们具有均匀的类别分布，则熵最大。

为了更直观地理解熵，让我们为类别 1 的概率范围[0，1]绘制杂质指数。代码如下:

![](img/d209b57d187666d07b4cb672b9dc5284.png)

可以看到，如果 *p(i=1|t) = 1* ，熵就是 0。如果类以 *p(i=1|t) = 0.5* 均匀分布，熵为 1。

现在，回到我们的虹膜例子，我们将可视化我们训练过的分类树，看看熵是如何决定每个分裂的。

`scikit-learn`的一个很好的特性是，它允许我们在训练后将决策树导出为一个`.dot`文件，例如，我们可以使用 [GraphViz](http://www.graphviz.org/) 将其可视化。除了 GraphViz，我们将使用一个名为`pydotplus`的 Python 库，它具有与 GraphViz 类似的功能，允许我们将`.dot`数据文件转换为决策树图像文件。

您可以通过在终端中执行以下命令来安装`pydotplus`和`graphviz`:

```
pip3 install pydotplus
apt install graphviz
```

以下代码将创建一个 PNG 格式的决策树图像:

![](img/4c3c73913cbe58c308b373a7d1e2b43a.png)

tree.png

查看保存在图像文件`tree.png`中的结果决策树图，我们现在可以很好地追溯决策树从我们的训练数据集确定的分裂。我们从根处的 150 个样本开始，使用**花瓣宽度**截止值≤ 1.75 cm，将它们分成 50 个和 100 个样本的两个子节点。第一次拆分后，我们可以看到左边的子节点已经是纯的，只包含来自`setosa`类的样本(熵= 0)。右侧的进一步分割用于从`versicolor`和`virginica`类别中分离样本。

查看最终的熵，我们看到深度为 4 的决策树在分离花类方面做得非常好。

# 回归树

我们将使用 [*波士顿住房*](https://www.cs.toronto.edu/~delve/data/boston/bostonDetail.html) 数据集作为我们的回归示例。这是另一个非常受欢迎的数据集，包含波士顿郊区的房屋信息。共有 506 个样本和 14 个属性。出于简单和直观的目的，我们将只使用两个目标值— `MEDV`(以千美元计的自有住房的中值)和`LSTAT`(人口中较低地位的百分比)作为特征。

让我们首先将必要的属性从`scikit-learn`导入到`pandas`数据框架中。

![](img/2d2afe3a16fab2dd23b3fb26354bf4c1.png)

让我们使用在`scikit-learn`中实现的`DecisionTreeRegressor`来训练一个回归树:

请注意，我们的`criterion`与我们用于分类树的不同。熵作为杂质的量度是分类的有用标准。然而，为了使用决策树进行回归，我们需要适用于连续变量的杂质度量，因此我们使用子节点的**加权均方误差** ( **MSE** )来定义杂质度量:

![](img/eff64c7e1477d4839403bee87a93fc98.png)

这里， *Nt* 为节点 *t* 的训练样本数， *Dt* 为节点 *t* 的训练子集， *y(i)* 为真实目标值， *ŷt* 为预测目标值(样本均值):

![](img/51593def1b80dda6baaf037be9718ded.png)

现在，让我们对`MEDV`和`LSTAT`之间的关系进行建模，看看回归树的直线拟合看起来像什么:

![](img/20ef8c0192077d88f4a059f6fa1b0868.png)

正如我们在结果图中看到的，深度为 3 的决策树捕捉到了数据的总体趋势。

我希望你喜欢这个关于决策树的教程！我们讨论了决策树的基本概念，最小化杂质的算法，以及如何为分类和回归构建决策树。

在实践中，知道如何为树的深度选择一个合适的值以避免数据过拟合或欠拟合是很重要的。了解如何组合决策树以形成集合**随机森林**也很有用，因为由于随机性，它通常比单个决策树具有更好的泛化性能，这有助于减少模型的方差。它对数据集中的异常值也不太敏感，并且不需要太多的参数调整。

*我们在我们的* ***Python 机器学习*** *系列中涵盖了这些技术，以及其他机器学习模型，如感知器、Adaline、线性和多项式回归、逻辑回归、支持向量机、核支持向量机、k 近邻、情感分析模型、k 均值聚类、DBSCAN、卷积神经网络和递归神经网络。*

*我们还关注其他主题，如正则化、数据处理、特征选择和提取、降维、模型评估、集成学习技术以及部署机器学习模型。*

*这里* *可以入门* [*！*](https://c.next.tech/2E7k6Dy)