# 贝叶斯网络中的信念传播

> 原文：<https://towardsdatascience.com/belief-propagation-in-bayesian-networks-29f51fdc839c?source=collection_archive---------6----------------------->

## 贝叶斯网络推理

在本文中，我将使用信念传播(BP)和一些示例数据。我假设你已经知道贝叶斯网络(BN)。这篇文章解释了如何计算 BN 中帮助推理的不同变量的信念。

![](img/17bdbc976018fc8e2a919cde0a6c2fee.png)

Photo by [Clint Adair](https://unsplash.com/@clintadair?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 信念传播

我在 [GitHub](https://github.com/wenig/belief_propagation) 上用 BP 的代码创建了一个存储库，我将用它来解释算法。

首先，假设我们有一棵没有环的多叉树。例如，下图所示的图表。我们有 4 个变量“雨”、“洒水器”、“福尔摩斯”和“华生”，有向边“雨”到“福尔摩斯”、“雨”到“华生”和“洒水器”到“福尔摩斯”。贝叶斯网络模拟了福尔摩斯和华生成为邻居的故事。一天早上，福尔摩斯走出家门，发现草地是湿的。不是下雨了，就是他忘了关洒水器。所以他去邻居沃森那里看看他的草是不是也湿了。当他看到确实是湿的，他很肯定他没有忘记洒水器，而是下雨了。所以信息从沃森流向洒水器。这个信息流在 BNs 中用 BP 建模。

在 BP 中，我们让变量彼此交谈，以交换它们对彼此的信念。有两种信息:父母给孩子的信息和孩子给父母的信息。总的来说，我们只需要使用 5 个公式来做 BP。在我的解释中，我将对某些公式和变量使用不同的名称，因为我发现一些来源相当误导。

## 1.可能性

似然性保存关于儿童观察的信息，例如，霍姆斯草地未被观察的似然性是 1 表示潮湿，1 表示不潮湿。如果观察到潮湿的草地，则潮湿的可能性变为 1，不潮湿的可能性变为 0。这些单位向量不是归一化的。

![](img/8b75d965cbcaf33ae5f0ebcc4adbf8aa.png)

Likelihood function is a product of all incoming messages from a variables children

可能性函数基本上是一个变量的子变量发送的所有传入消息的乘积。它返回一个似然向量，包含变量的每个可能值的似然值。在“雨”的情况下，它的基数为 2，代表两种状态“是”和“否”。

如果变量没有子节点，因为它是图中的叶节点并且没有被观察到，那么它的似然向量将是单位向量，对于它的所有可能值都是 1，例如，由于我们在开始时没有观察到霍姆斯的草地，所以我们将它的似然向量分别设置为[1，1]用于“不湿”和“湿”。

在 Python (numpy)代码中是这样的。

```
**def likelihood**(self):
    incoming_children_messages = np.array([
        c.message_to_parent(self) **for** c **in** self.children
    ])
    **return** incoming_children_messages.prod(axis=**0**)
```

## 2.传道者

先验是在开始时已经知道的某些事件的概率，例如，下雨的概率为 20%。如果先验是未知的，下面的公式是计算它。这有点复杂，但我会试试看。先验给出了各个变量的无条件概率。因此，我们也需要包含条件变量。

![](img/3b646890f8b6314e6f413292ca310f36.png)

Prior probability function is the sum of all possible combinations of parent values times the product of the respective incoming messages

在我们的例子中也给出了条件概率。在公式中，“P(X|W)”对应于此。此外，我们需要使用来自所有父母的传入消息，这就是公式中的“ϕ”。索引显示了消息方向——从父变量“K”到当前变量“X”。使用这两个部分(条件概率和来自父母的信息),因为它们都给出了关于变量概率的信息。一方面，我们看到给定一些父母值的概率，另一方面，我们看到那些父母的消息。不用观察，这些信息对应着父母的前科。因此，这里，正在计算“X”的**余量**，并去掉条件变量。

对于每个父母的消息，在条件概率中存在相应的部分。因此，我们可以用条件概率表对每条消息执行点积，在这个代码片段中是 *self.m* 。

```
**def** **priors**(self):
     parents_messages = [
         p.message_to_child(self) **for** p **in** self.parents
     ]
     **return** reduce(np.dot, [self.m.transpose()]+parents_messages)
```

## 3.相信

信念是我们观察到某些事件后的后验概率。它基本上是可能性和先验的标准化产物。

![](img/11d35d4ea8af435331a93ed5edfef51e.png)

Belief is the normalized product of the likelihood and prior

我们采用我们事先知道的概率，并引入从孩子们那里获得的新知识。这样，我们就对变量产生了新的信念。如果一个变量既有父变量又有子变量，那么信念就是包含上下信息的更新概率(后验概率)。因此每个传入的消息都被考虑在内。“α”是一个归一化常数，因为似然性和先验的乘积总和可能大于 1。这是一种用变量所有可能状态的总和进行除法运算的简写形式。

在这个 Python 片段中，规范化部分变得更加清晰。

```
**def** **belief**(self):
     unnormalized = self.likelihood() * self.priors()
     normalized = unnormalized/unnormalized.sum()
     **return** normalized
```

## 4.给父母的信息

为了计算一个变量的可能性，我们需要考虑来自一个变量的子变量的所有传入消息，这些子变量由可能性函数中的λ表示。

![](img/033114b47cb1a56b7735cd9b15bd2abd.png)

这个公式相当混乱，但是在查看一些 Python 代码时更容易理解。一般来说，我们从 P(X|U)中边缘化掉 k，而 x 是发送者(孩子)，k 是接收者(父母)，u 是 x 的所有父母，包括 k。如果我们为 x 设想一个条件概率表，对于每个条目，我们取父母的相应激活，并乘以各自的传入消息ϕ，而不包括 k 本身。然后，我们将这个值乘以 X 的可能性。最后，我们对 K 值相同的所有值求和，剩下一个向量，它是从 X 到 K 的信息。

因此，给父母的消息会考虑所有传入的消息，不管它们是由孩子还是父母发送的(除了接收消息的父母)，并考虑给定特定父母值的概率。因此，概率高的变量设置比概率低的变量设置更容易转发传入的消息。根据消息设置的条件概率对传入消息进行评级。

我希望 Python 代码能进一步阐明这一点。

```
**def** **message_to_parent**(self, parent):
    likelihood = self.likelihood()
    parents_priors = np.array([
        p.message_to_child(self) 
            **for** p **in** self.parents **if** p != parent
    ])
    parent_i = self.parents.index(parent)

    stack = np.vstack([
        np.dot(
            self.m.take(r, axis=parent_i).transpose(),    
            parents_priors.prod(axis=**0**)
        ) 
        **for** r **in** range(parent.cardinality)
    ])
    **return** np.dot(stack, likelihood)
```

或者举个福尔摩斯的例子:

```
message = np.zeros(rain.cardinality)
**for** r **in** rain:
  **for** s **in** sprinkler:
    **for** h **in** holmes:
      message[r] = probas[r, s, h] \
                   * sprinkler_message[s] \
                   * likelihood[h]
```

## 5.给孩子们的信息

要计算父母发给孩子的信息，有两种方法。从其它子节点接收的所有消息与当前节点的先验相乘，或者当前节点的信念除以相应子节点给父节点的消息。

![](img/e38a6863acf4adea8eda1ff4b25bfffa.png)

我们认为这个公式叫做 Kappa，它的索引告诉我们信息的方向(从 X 到 K)。

如果我们看看信念的公式，我们看到这个公式是可能性和先验的乘积。然而，可能性是所有传入消息的乘积。因此，信念除以来自 K 的传入消息得到所有传入消息——除了我们除以的那个消息——和先前消息的乘积。这样，我们就可以解释计算 Kappa 的两种方法之间的相等性。传递给孩子们的信息背后的直觉与传递给父母的信息相似。您考虑了所有传入的消息(因此考虑您可以获得的所有信息),并将聚合发送到下一个节点。

α也是一个归一化常数。如果父节点只有一个子节点，它就不能从其他子节点收集消息，因为没有子节点。因此，它将只返回它的 prior。

```
**def** **message_to_child**(self, child):
    children_messages = []
    **for** c **in** self.children:
        **if** c != child:
            children_messages.append(c.message_to_parent(self))
    **if** len(children_messages) > **0**:
        unnormalized = (children_messages * self.get_priors())
        unnormalized = unnormalized.prod(axis=**0**)
        message = unnormalized/unnormalized.sum()
        **return** message
    **return** self.get_priors()
```

# 例子

利用我在开始提到的知识库，我们现在可以用霍姆斯的例子，计算不同情况下的信念。

为了使用这个库，我们需要将它和 NumPy 库一起导入。

```
**import** **numpy** **as** **np**
**from** **node** **import** Node
```

我们导入了存储库的节点类，它代表了 BN 中的单个节点。在下一步中，我们实际上创建了代表单个概率变量的节点:“福尔摩斯的草地是湿的”、“下过雨的”、“忘记洒水器了”和“沃森的草地是湿的”。创建节点时，必须提供一个名称。之后，您需要设置一些属性，如基数、先验或可能性(如果存在)。

```
rain = Node("rain")
rain.cardinality = **2**
rain.priors = np.array([**0.8**, **0.2**]) #  no=0 yes=1

sprinkler = Node("sprinkler")
sprinkler.cardinality = **2**
sprinkler.priors = np.array([**0.9**, **0.1**]) #  no=0 yes=1
```

对于没有子节点的节点，这很简单。对于其他节点，它们有父节点，但没有可用的先验，我们需要定义一个条件概率表(CPT ),它定义了给定来自父节点的所有可能输入时变量的概率。这个 CPT 在代码中称为“m”。

```
m = np.zeros((**2**, **2**, **2**)) #  rain, sprinkler, holmes' grass
m[**1**, **1**, **1**] = **1**
m[**0**, **1**, **1**] = **0.9** #  <-- here
m[**0**, **1**, **0**] = **0.1**
m[**1**, **0**, **1**] = **1**
m[**0**, **0**, **0**] = **1**
holmes = Node("holmes")
holmes.cardinality = **2**
holmes.m = m
holmes.likelihood = np.array([**1**, **1**])

m = np.zeros((**2**, **2**)) # rain, watson's grass
m[**1**, **1**] = **1**
m[**0**, **1**] = **0.2**
m[**0**, **0**] = **0.8**
watson = Node("watson")
watson.cardinality = **2**
watson.m = m
watson.likelihood = np.array([**1**, **1**])
```

正如你所看到的，“m”在矩阵的第一个维度中取父元素的值，在最后一个维度中取实际变量的值，例如(代码注释中的“here”)如果没有下雨(0)并且忘记洒水器(1)，那么草地潮湿的概率(1)是 0.9。草地潮湿的可能性是 1，1，这意味着两种状态具有相同的可能性。

接下来，我们必须连接节点来定义因果关系。Node 类有一个名为“add_parent”的方法，它可以将变量连接到父变量。

```
holmes.add_parent(rain)
holmes.add_parent(sprinkler)
watson.add_parent(rain)
```

在接下来的步骤中，我们假设福尔摩斯的草地是湿的(因此，可能性[0，1])。然后，我们想知道沃森的草是否也是湿的(或者湿的可能性有多大)。

```
holmes.likelihood = np.array([**0**, **1**])
holmes.message_to_parent(rain)
holmes.message_to_parent(sprinkler)
watson.get_belief() #  array([0.21176471, 0.78823529])
```

我们看到，沃森的草是湿的这一信念确实是趋向于湿的(0.21 vs 0.79)。因此，BN 预计 Watson 的草地是湿的，因为在雨节点上有连接，通过它信仰被传播。

# 结论

BNs 的工具集在推理案例时非常有用，如下所示。我真的对因果推理的整个研究领域感到兴奋，并认为在深度学习和普通人工智能方面也会取得很多进展。

# 参考

此处的示例取自。