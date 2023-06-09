# 用 TensorFlow.js 构建一个简单的神经网络

> 原文：<https://towardsdatascience.com/build-a-simple-neural-network-with-tensorflow-js-d434a30fcb8?source=collection_archive---------13----------------------->

## 创建一个神经网络模型来做出笔记本电脑购买决策

![](img/d14c224fea61af12d27dda5a73d2465d.png)

> *TL；DR 在 TensorFlow.js 中建立一个简单的神经网络模型，做出笔记本电脑购买决策。了解为什么神经网络需要激活函数，以及应该如何初始化它们的权重。*

现在是午夜，你正微笑着做着一些令人惊恐的梦。突然，你的电话开始响了，相当国际化。你半睡半醒地拿起电话，听一些奇怪的事情。

你的一个朋友从地球的另一边打电话来，请求帮助挑选一台笔记本电脑。毕竟今天是黑色星期五！

这是你五年来第一次收到朋友的来信，这让你有点惊讶。不过，你是个好人，同意帮忙。也许是时候将你的 TensorFlow.js 技能付诸实践了？

不如你做一个模型来帮助你的朋友，这样你就可以继续睡觉了？你听说过神经网络现在非常热门。现在是凌晨 3 点，你不需要太多的劝说。这一次你将使用神经网络！

**在你的浏览器中运行本教程的完整源代码:**

[GitHub 上的完整源代码](https://github.com/curiousily/Simple-Neural-Network-with-TensorFlow-js)

# 神经网络

什么是神经网络？按照经典的扣人心弦的方式，我们将从远离回答这个问题开始。

神经网络已经存在了一段时间(从 20 世纪 50 年代开始)？为什么它们最近才变得流行起来(最近 5-10 年)？由沃伦·麦卡洛克和沃尔特·皮茨于[年首次提出的神经活动固有思想的逻辑演算](https://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf)神经网络直到 20 世纪 80 年代中期才真正流行起来，当时[支持向量机](https://en.wikipedia.org/wiki/Support_vector_machine)和其他方法控制了整个社区。

[通用逼近定理](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.101.2647&rep=rep1&type=pdf)指出，神经网络可以逼近任何函数(在一些温和的假设下)，即使只有一个隐藏层(稍后将详细介绍)。第一批证明之一是由乔治·西本科于 1989 年为乙状窦激活函数做的。

最近，深度学习领域越来越多的进展使得神经网络再次成为热门话题。为什么？我们稍后会讨论这个问题。首先，我们从基础开始！

# 感知器

最初的模型是由弗兰克·罗森布拉特在 20 世纪 50 年代提出的，旨在模拟人类大脑如何处理视觉数据和学习识别物体。感知器接受一个或多个二进制输入 x1，x2，…，xn，并产生一个二进制输出:

要计算输出，您必须:

*   具有表示相应输入的重要性的权重 w1、w2、…、wn
*   二进制输出(0 或 1)取决于加权和∑ wj xj 是大于还是小于某个阈值

![](img/dc63c4b53752c86285ff094ef096c7a1.png)

让我们看一个例子。假设您需要决定是否需要一台新的笔记本电脑。最重要的特征是它的颜色和大小(她是这么说的)。因此，您有两个输入:

1.它是粉红色的吗？

2.它小吗(明白了)？

![](img/a7f9493889c388798507b3ff2702c9fd.png)

你可以用二元变量 x_ *pink* ，x_ *small* 来表示这些因素，并给每一个赋予权重/重要性 w_ *pink* ，w_ *small* 。根据你对每个因素的重视程度，你可以得到不同的模型。

我们可以进一步简化感知器。我们可以将∑ w_j x_j 重写为两个向量 w . x 的点积，接下来，我们将引入感知机的偏差，b = -threshold。使用它，我们可以将模型重写为:

![](img/6a45a04dfa815a8daa2d6a553e852313.png)

偏差是衡量感知器输出 1(触发)的难易程度。较大的正偏置使输出 1 变得容易，而较大的负偏置使输出 1 变得困难。

让我们使用 TensorFlow.js 构建感知器模型:

有人出价购买笔记本电脑。它不是粉红色的，但它是小 x = [0，1]。你偏向于不买笔记本电脑，因为你破产了。你可以用负偏压来编码。你是一个比较聪明的用户，你更注重尺寸，而不是颜色 w = [0.5，0.9]:

1

是的，你必须买那台笔记本电脑！

# 乙状结肠神经元

为了使从数据中学习成为可能，我们希望在给出一个例子时，模型的权重只发生少量的变化。也就是说，每个示例都会导致输出发生微小的变化。

这样，人们可以在呈现新数据的同时不断调整权重，而不必担心单个示例会抹去模型迄今为止已经学习的所有内容。

感知器不是理想的，因为输入的小变化会线性传播到输出。我们可以使用一个*s 形*神经元来克服这个问题。

乙状结肠神经元具有输入 x1，x2，…，xn，其值可以在 0 和 1 之间。输出由σ(w . x + b)给出，其中σ为 *sigmoid 函数*，定义如下:

![](img/c690d43c0e394d65a8c56203bfa5e754.png)

让我们用 TensorFlow.js 和 Plotly 来看看:

![](img/e3e2925070b7532864bf687dbc3777df.png)

使用权重和输入，我们得到:

![](img/2e97716843195b4dee88a08552710f29.png)

让我们更深入地了解乙状结肠神经元，并理解它与感知器的相似之处:

*   假设 z 是一个大的正数。那么 e^{-z} ≈ 0，σ(z) ≈ 1
*   假设 z 是一个大的负数。那么 e^{-z} → ∞，σ(z) ≈ 0
*   当 z“有些适度”时，我们观察到与感知器相比的显著差异。

![](img/524daa111107cffa0e1d707f8615d648.png)

让我们使用 TensorFlow.js 构建 *sigmoid 神经元*模型:

另一个笔记本电脑的报价出现了。这一次你可以指定颜色接近粉红色的程度，以及它有多小。

颜色有些粉，大小刚好 x = [0.6，0.9]。其余的保持不变:

*0.6479407548904419*

是的，你还是想买这款笔记本电脑，但是这款也输出了其决策的自信。很酷，对吧？

# 构建神经网络

扩展上述模型的一个自然方法是以某种方式将它们分组。一种方法是制造多层神经元。这里有一个简单的神经网络，可以用来做出购买笔记本电脑的决定:

![](img/7c0cb19c7d5e53082119724303462a92.png)

神经网络是神经元的集合，连接在一个非循环图中。一些神经元的输出被用作其他神经元的输入。它们被组织成层。我们的示例由全连接层(两个相邻层之间的所有神经元都是连接的)组成，它是一个 2 层神经网络(我们不计算输入层)。由于构建神经网络的神经元做出的简单决定的组合，神经网络可以做出复杂的决定。

当然，输出图层包含您正在寻找的答案。让我们来看看使训练神经网络成为可能的一些因素:

**激活功能**

感知器模型只是一个线性变换。将多个这样的神经元相互堆叠会导致矢量积和偏差相加。不幸的是，有很多函数不能通过线性变换来估计。

激活函数使模型能够逼近非线性函数(预测更复杂的现象)。好消息是，你已经遇到了一个激活函数 sigmoid:

![](img/e3e2925070b7532864bf687dbc3777df.png)

Sigmoid 函数的一个主要缺点是，它在[-3，+3]范围之外变得非常平坦。这导致权重接近 0——没有学习发生。

**ReLU**

ReLU，在[整流线性单元的神经网络环境中引入，改进受限玻尔兹曼机器](https://www.cs.toronto.edu/~hinton/absps/reluICML.pdf)，在大于 0 和 0 的值处具有线性输出。

让我们来看看:

![](img/b73c9e2270a76b079398ded63f1db5df.png)

ReLU 的一个缺点是负值“消亡”，停留在 0——没有学习。

**泄漏的 ReLU**

[整流器非线性改善神经网络声学模型](https://ai.stanford.edu/~amaas/papers/relu_hybrid_icml2013_final.pdf)中引入的泄漏 ReLU 解决了 ReLU 引入的死值:

![](img/7272e1c616510e8b00d0d0ffebf40a96.png)

请注意，负值会被缩放，而不是清零。缩放可通过 [tf.leakyRelu()](https://js.tensorflow.org/api/latest/#leakyRelu) 中的参数进行调整。

# 重量初始化

训练神经网络做出“合理”预测的过程包括多次调整神经元的权重。这些权重需要有初始值。你应该如何选择那些？

初始化过程必须考虑我们用来训练模型的算法。通常，这个算法是[随机梯度下降(SGD)](https://en.wikipedia.org/wiki/Stochastic_gradient_descent) 。它的工作是搜索可能的参数/权重，并选择那些使我们的模型产生的误差最小的参数/权重。此外，该算法严重依赖于随机性和良好的起点(由权重给出)。

**相同常数初始化**

假设我们使用相同的常数(是的，包括 0)初始化权重。网络中的每个神经元将计算相同的输出，这导致相同的权重/参数更新。我们刚刚挫败了拥有多个神经元的目的。

**过小/过大值初始化**

让我们用一组小值初始化权重。将这些值传递给激活函数将使它们呈指数级下降，从而使每个权重都变得同等重要。

另一方面，用大值初始化将导致指数增长，使得权重同样不重要。

**随机小数字初始化**

我们可以使用平均值为 0、标准偏差为 1 的[正态分布](https://en.wikipedia.org/wiki/Normal_distribution)用小随机数初始化权重。

每个神经元会计算不同的输出，从而导致不同的参数更新。当然，还有其他多种方式。检查 [TensorFlow.js 初始化器](https://js.tensorflow.org/api/latest/#Initializers)

# 你应该买笔记本电脑吗？

现在你已经知道了一些神经网络的功夫，我们可以使用 TensorFlow.js 来建立一个简单的模型，并决定你是否应该购买一台给定的笔记本电脑。

**笔记本电脑数据**

这么说吧，对于你的朋友来说，大小比粉嫩程度重要多了！你坐下来设计以下数据集:

干得好！你在整合朋友偏好方面做得很好。

**建立模型**

回想一下我们将要构建的神经网络:

![](img/7c0cb19c7d5e53082119724303462a92.png)

让我们将其转换为 TensorFlow.js 模型:

我们有一个 *2 层网络*，输入层包含 *2* 个神经元，隐藏层包含 *3* 个神经元，输出层包含 *2* 个神经元。

注意，我们在隐藏层使用 ReLU 激活函数，在输出层使用 softmax。我们在输出层有 2 个神经元，因为我们想知道我们的神经网络在购买/不购买决策中有多确定。

我们使用[二元交叉熵](https://peltarion.com/knowledge-center/documentation/modeling-view/build-an-ai-model/loss-functions/binary-crossentropy)通过测量预测的“好”程度来衡量我们模型的当前权重/参数的质量。

我们的训练算法，[随机梯度下降](https://en.wikipedia.org/wiki/Stochastic_gradient_descent)，试图找到使损失函数最小化的权重。对于我们的例子，我们将使用 [Adam 优化器](https://js.tensorflow.org/api/latest/#train.adam)。

**培训**

既然我们的模型已经定义，我们可以使用我们的训练数据集来教授它关于我们的朋友偏好的信息:

我们在训练前重组数据，并在每个时期完成后记录进度:

```
Epoch 1
Loss: 0.703386664390564 accuracy: 0.5
Epoch 2
Loss: 0.6708164215087891 accuracy: 0.5555555820465088
Epoch 3
Loss: 0.6340110898017883 accuracy: 0.6666666865348816
Epoch 4
Loss: 0.6071969270706177 accuracy: 0.7777777910232544
...
Epoch 19
Loss: 0.08228953927755356 accuracy: 1
Epoch 20
Loss: 0.06922533363103867 accuracy: 1
```

在经历了大约 20 个时期之后，这个模型似乎已经了解了你朋友的偏好。

**评价**

你保存模型，并将其发送给你的朋友。连接到您朋友的计算机后，您找到一台合适的笔记本电脑，并将信息编码到模型中:

等待几毫秒后，您会收到一个回答:

```
0: 0.45
1: 0.55
```

这个模型适合你。它“认为”你的朋友应该购买笔记本电脑，但它对此并不确定。你做得很好！

# 结论

你的朋友似乎对结果很满意，而你正考虑通过将你的模型作为浏览器扩展来销售，从而赚上百万。不管怎样，你学到了很多:

*   感知器模型
*   为什么需要激活功能，使用哪一个
*   如何初始化神经网络模型的权重
*   建立一个简单的神经网络来解决一个(有点)实际的问题

**在浏览器中运行本教程的完整源代码:**

[GitHub 上的完整源代码](https://github.com/curiousily/Simple-Neural-Network-with-TensorFlow-js)

躺在舒适的枕头上，你开始思考。我可以用深度学习来做这个吗？

# 参考

[减少损失:梯度下降](https://developers.google.com/machine-learning/crash-course/reducing-loss/gradient-descent)

[梯度下降和随机梯度下降从零开始](https://gluon.mxnet.io/chapter06_optimization/gd-sgd-scratch.html)

[初始化神经网络](https://www.deeplearning.ai/ai-notes/initialization/)

[重量初始化的类型](https://www.deeplearningwizard.com/deep_learning/boosting_models_pytorch/weight_initialization_activation_functions/#types-of-weight-intializations)

[如果不使用神经网络中的任何激活函数会怎样？](https://stats.stackexchange.com/questions/267024/what-if-do-not-use-any-activation-function-in-the-neural-network)

*原载于*[*https://www.curiousily.com*](https://www.curiousily.com/posts/build-a-simple-neural-network-with-tensorflow-js/)*。*

建立机器学习模型(特别是深度神经网络)，可以轻松地与现有或新的 web 应用程序集成。想想您的 ReactJs、Vue 或 Angular 应用程序通过机器学习模型的强大功能得到了增强:

[](https://leanpub.com/deep-learning-for-javascript-hackers) [## JavaScript 黑客的深度学习

### 建立机器学习模型(特别是深度神经网络)，您可以轻松地与现有或新的网络集成…

leanpub.com](https://leanpub.com/deep-learning-for-javascript-hackers)