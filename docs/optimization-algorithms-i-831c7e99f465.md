# 优化算法 I

> 原文：<https://towardsdatascience.com/optimization-algorithms-i-831c7e99f465?source=collection_archive---------18----------------------->

## 新加坡元和动量

我们将有一个简短的优化概述，因为为什么需要它，稍后我们将讨论几个突出的算法。

为什么我们需要优化算法？

机器学习中的所有问题，无论是回归还是分类，都有一个要达到最佳性能的目标。模型的好坏与预测的好坏直接相关，即对于分类问题，模型应该能够正确地识别事物，而对于回归问题，模型的预测应该足够接近真实值。为了开发一个“好模型”，我们通常会将经验风险与问题联系起来，并试图通过迭代过程来降低它。机器学习优化算法与其他优化算法的一个重要区别是，它们不会在达到局部最小值后停止，而是在满足停止标准时停止。在深度学习和一般人工神经网络中，我们可能经常使用代理损失函数而不是经验风险最小化，因为它们容易过度拟合。

神经网络训练面临额外的问题。由于导致非常慢的步骤的病态 Hessian 矩阵、可能与局部最小值混淆的鞍点以及使训练不稳定的爆炸梯度，可能会出现问题。此外，使用小批训练样本的梯度近似可能导致不精确的估计，并使梯度在不同于最佳方向的方向上移动，所述最佳方向可能是利用整个数据集上的梯度获得的。

虽然 SGD 是经典的，并且仍然可以在许多问题中找到应用，但是使用自适应算法已经成为一种趋势。

## **1。随机梯度下降**

对于初学者来说，随机梯度下降是一个容易理解的算法。它在许多方面类似于其前身批量梯度下降，但在某种意义上提供了一个优势，即它通过更少的数据集在降低风险目标方面取得了快速进展。算法如下:

![](img/becabcd65906f0ce5e7186c9fccbbc7f.png)

该算法本质上是在每次迭代中选择 m 个数据点，计算它们的平均梯度，更新参数，并对各种学习速率这样做以获得最佳模型。它重复这个过程，直到满足某个收敛标准。

***为什么我们需要改变学习率？*** 训练样本的随机采样给梯度增加了随机噪声，即使在局部最小值时也不会减少。因此，为了保证收敛，我们允许学习率在一些初始迭代中降低，并在之后保持不变。保证收敛的充分条件是，

![](img/a591156988e78972b1f170a7f69f99fb.png)

matcha.io

这里，ε-k 是第 k 次迭代后的学习率。

![](img/f52649bcc3dd857df2b6d446999c741b.png)

mathcha.io

根据深度学习的书，我们将ε的最终固定值设定为初始值的 1%左右。SGD 的一个重要性质是每次迭代的参数更新仅取决于批量 m，因此每次迭代的计算时间不随训练样本数量的增加而改变。对于一个凸问题，推广误差(当前迭代后损失函数值与损失函数值最小值之差)每一步递减`O(1/sqrt(k))`。根据 Cramer-Rao 界，这种推广误差在一次迭代中不能减少超过 `O(1/k)`。

## **2。势头**

使用 SGD 的动量来克服与 SGD 相关的病态 Hessian 矩阵和梯度方差的问题。它通过保持梯度的移动平均值来实现这一目标。现在，更新不仅依赖于当前梯度，而且依赖于来自过去的梯度序列。它基本上维护另一个变量 v，该变量将累积梯度，并使用该变量来更新参数。算法如下:

![](img/c95127d573b36dc1f204d0725427ffb5.png)

Momentum with SGD

需要注意的重要一点是，我们现在要考虑另一个超参数。在下图中，红线显示了渐变随动量的移动。它更快，更直接地指向目标，因为它一直在考虑过去梯度的方向，并通过平均它们。等高线代表平方损失函数

![](img/5fa41a0aba0d76053cb782089f782cd4.png)

## 参考资料:

 [## 深度学习

### 深度学习教材是一个资源，旨在帮助学生和从业人员进入机器领域…

www.deeplearningbook.org](https://www.deeplearningbook.org/) 

即将推出自适应方法的优化算法 2。