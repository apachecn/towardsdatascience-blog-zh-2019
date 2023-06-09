# 通过矩阵分解开发一个规范的推荐系统

> 原文：<https://towardsdatascience.com/developing-a-prescriptive-recommender-system-through-matrix-factorization-8b0c69cce611?source=collection_archive---------16----------------------->

*作者——拉温德拉·舒克拉(人工智能/人工授精从业者)*

**摘要—** 矩阵分解是一种非常强大的算法，在多个行业中有许多有价值的用例。矩阵分解的一些众所周知的应用是——网飞 100 万美元的电影推荐奖和亚马逊在线应用(非常精炼的版本),用于向各种读者推荐书籍。虽然这是一种非常流行的方法，但它有一些局限性。我们在本文中的重点是了解潜在的因素，以及如何使其更具规范性。当集合中的产品已经被少数用户评价或者每个用户已经评价了少数产品时，该算法工作得很好。然而，如果我们在集合中包括没有被任何用户评级的新产品或者集合中对产品的偏好未知的新用户，那么将很难为未评级的产品和新用户创建推荐。基于关键特征将产品的潜在特征和用户偏好相关联是一个挑战。下面的文章提出了解释与产品和用户特征相关的潜在因素的挑战。一旦我们对产品和用户特性有了清晰的认识——我们就可以走向规定性的旅程。这将有助于设计具有更受欢迎功能的未来产品，或为某一特定产品找到市场。

**背景—** 对于基本术语和背景的理解，我一般会引用维基百科。

矩阵分解是[推荐系统](https://en.wikipedia.org/wiki/Recommender_systems)中使用的一类[协同过滤](https://en.wikipedia.org/wiki/Collaborative_filtering)算法。矩阵分解算法通过将用户-项目交互矩阵[分解成两个低维度矩形矩阵的乘积来工作。](https://en.wikipedia.org/wiki/Matrix_(mathematics))

[https://en . Wikipedia . org/wiki/Matrix _ factorization _(recommender _ systems)](https://en.wikipedia.org/wiki/Matrix_factorization_(recommender_systems))

我们总是需要将身边的两个实体联系起来。想想各种场景——病人对疾病，用户对产品，男人对女人，用户对电影偏好，求职者对空缺职位。我们可以将这个概念扩展到日常生活中的许多其他场景，并找到相关性。当我们试图寻找两个实体之间的相关性时，矩阵分解非常方便。

**矩阵分解的使用案例-**

市场战略

交叉销售和追加销售

计算产品倾向和客户倾向

推荐引擎/个性化

推出新产品

了解客户 360

求职网站的筛选和推荐

婚姻或约会网站中的过滤和推荐

上面的场景只是几个例子，这个概念是非常通用的，并且有广泛的使用范围。

**创新使用** —事实上，在我们之前的一个项目中，我们使用矩阵分解来填充数据集中缺失的值。这个练习是为了计算健康分数(一个非常类似于信用分数的概念——健康分数越高表示健康状况越好)。假设我们缺少一个患者(P1)的 A1C 读数，我们可以将其他具有类似特征(年龄、性别、身体质量指数、人口统计学、血压、胆固醇、生活方式等)的患者与患者 P1 相关联，并相应地估计 P1 的 A1C 读数。

**机器学习基础——矩阵和向量的使用**

在我们深入研究矩阵分解和如何解释潜在因素之前，让我们先了解一些机器学习的基础知识。

机器学习是基于数学的，它涉及基于梯度下降(【https://en.wikipedia.org/wiki/Gradient_descent】)的迭代优化，以最小化预测中的误差。存储在数据库中的数据不能作为输入传递给算法，它需要用矩阵来表示。矩阵是不同向量的组合，在定义数学运算时很有用。

用户可能具有以下特征——用户 id、用户名、地址、年龄、性别、收入、教育、对产品特征的偏好、用户类型(学生、工人、IT 工人、销售人员)

类似地，我们可以根据患者的生物特征来定义他/她的基本特征。

像笔记本电脑这样的产品将具有诸如触摸屏、RAM、CPU、品牌、颜色、成本(范围)等特征。像一本书这样的产品将具有诸如作者、主题、时期写作、流派、诗歌与散文、小说与非小说、长篇与短篇、精装与软装、纸质书与电子书、技术书籍等特征

但是，我们不能像在机器学习算法中那样使用上述数据。数据需要以向量和矩阵的形式排列，以便我们在数学运算中可以将它们作为矩阵传递。

**用数学术语表示实体的实例—** 让我们看看如何用关键特征在 N 维中表示患者

**患者可能具有以下主要特征(样本)–**

患者 id —这是数据库中有用的唯一标识符。然而，机器学习和算法基于关键特征工作是不相关的。ID 只是数据库系统中的一个标识符。

姓名—类似于患者 id，在 ML 中没有意义

其他人口统计信息(种族、民族、婚姻状况、收入、教育和就业)

年龄—0 到 120 岁之间

性别——男性或女性

位置(州、国家)

生物计量读数(血压—收缩压(范围—0–200，舒张压—0–200)，血糖 0–400，A1C(0–10)，胆固醇(0–400)，吸烟—是或否，慢性病—是或否，共病—是或否)

它可以有更多的特性，但是上面的细节对于我们的讨论来说已经足够了。

**Epic 系统数据库中的患者记录-**

患者的实例(记录)将存储在常规数据库中，如下所示-

![](img/5a45cfe83c08911e68e48781619d1167.png)

A patient record in regular database

在 N 维中将患者表示为向量(P ),以便我们将其作为 ML 算法中的输入——

![](img/7899259a46eac89974636e27ddf44de2.png)

patient record with numeric values only

我们需要将所有文本数据转换成数字，并使其有意义，以便可以在计算中使用。有一种特殊的方法来扩展分类变量(例如，性别、州、共病等)。这个过程被称为 Onehotencoder。在数据预处理中还有许多其他活动，但是我们在这里不涉及这些细节(比如在调用 ML 算法之前归一化所有的值、清除丢失的数据等)。

患者实例的上述表示被称为 P 向量。我们组合患者向量的所有实例来创建患者矩阵 p。

**向量乘法是什么意思——**

将一个已知矩阵(评分矩阵)分解成两个未知矩阵(用户特征和产品特征)是矩阵分解的关键。让我们来理解两个矩阵(用户矩阵和乘积矩阵)相乘的意义是什么

A = a1.i + a2.j + a3.k —三维向量 A(假设—这是用户特征向量)

B = b1.i + b2.j + b3.k —三维向量 B(假设这是产品特征向量)

A x B = a1 . B1+a2 . B2+a3 . B3—A 和 B 向量的乘积

假设 I 代表安全性，j 代表家用车辆，k 代表产品和用户向量的性能系数。对于喜欢具有良好安全特性的高性能家用车辆的用户来说,( AxB)的值会更高。对于喜欢跑车且维护成本较高的用户来说，相同车辆的 AxB 值较低。我们可以清楚地看到，较高的 AxB 值将表明用户 A 对产品 b 的亲和力更好。让我们举个例子来理解——两个向量相乘的意义是什么。

尼鲁喜欢经典的动作片，由黑泽明执导，有很好的剧本、剪辑和背景音乐。她不喜欢恐怖、喜剧、悬疑或故事情节糟糕的电影。

![](img/d71972e4f4f8adf12b592e3dea2d8fe5.png)

User vector — Neeru — P1

![](img/17e889e79718c6d460fb1ea826593294.png)

Product vector Q1

![](img/31c9ac7155e8d6c01dc5b0a5b92d22d2.png)

Product vector — Q2

如果我们将两个向量相乘

P1(用户的 Neeru 实例)x Q1(七武士—产品实例)=(. 8x 1+. 1x 1.2+. 3x 5+. 9x 8+1x1+. 4x 0+. 4x 8+. 2x 2+. 7x 1)= 3.75

P1(用户的 Neeru 实例)x Q2(布莱尔女巫-产品的实例)=(. 8x . 2+. 1x . 8+. 3x . 3+. 9x . 4+1x 0+. 4x . 2+. 4x . 6+. 2x . 6+. 7x 0)= 1.13

这清楚地表明，比起布莱尔女巫，尼鲁更喜欢看七武士。

**解读潜在因素-**

矩阵分解基于下面的等式

**R = P x QT**

r 是不同用户对产品评级的矩阵

p 是用户矩阵

q 是乘积矩阵

QT 是矩阵 Q 的转置

我们没有产品和用户功能的细节。我们只有用户对各种产品的偏好(评分)(来自历史数据)。基本方法是—从假设产品和用户矩阵的某些系数开始，导出评级的预测值，找出预测值与实际值之间的差异作为误差，对误差求和，计算梯度以改变系数值，并再次重新计算预测值和误差。不断迭代，直到收敛到某个最小误差。所有这些都可以用 Python 中的 50 行代码来完成。

同样，上述带有量纲的方程可以写成-

**R [M，N] = P[M，K] x QT[K，N]**

R[i，j] —来自用户 i (Pi)的额定产品 j (Qj)的值

Q [i][1，2，3，…。k] =具有 k 个关键特征的乘积 Qi 向量
P[j][1，2，3，…。k] =由 k 个关键特征定义的用户 Pi 向量

我们假设在上面的等式中有 K 个潜在特征。

**潜伏因素有哪些？**

在矩阵分解中，我们的工作是将两个实体(例如产品和用户)。每个产品都有一些关键特征，每个喜欢该产品的用户都将取决于他/她对这些关键特征的偏好。

这些相关性中的许多可以通过矩阵分解来建立。当我第一次读到矩阵分解以及如何使用梯度下降来实现预测时，我很兴奋。用 python 写 50-60 行基本代码就能完成这么多事情。当我开始思考——如何让它更规范时，兴奋是短暂的。除非我们找到一种实用的方法来解释和扩展数学美，否则数学美就会消失。

我们做一个基本假设，两个实体通过 K 个潜在因素相关联。k 只是一个数字。我们不知道这些 K 因子代表什么。这就是为什么他们也被称为潜伏。这在使矩阵分解更规范方面造成了关键障碍。

我尝试了不同的组合来推导一些潜在因素的含义。其中之一是——不断增加 K 值，看看在某个数字之后，K 值的增加是否不会对用户和产品系数产生影响。用户系数和产品系数收敛，进一步增加 K 将无关紧要。它没有成功。

事实上，当我增加 K 值并尝试多次积分时，我开始得到矩阵 P 和 Q 系数的不同组合。

**破译矩阵分解-**

让我们用一个例子来分析一下细节。

r 矩阵—8 名用户对 4 种不同产品的评分。

![](img/658bd8c4f54c91cbcee18b64255a5a7e.png)

Rating Matrix — R

让我们假设——我们有四个潜在因素。换句话说，产品有 4 个主要特征，用户会根据这些关键特征对产品产生偏好。

**R [8x4] = P[8x4] X Q[4x4]**

**P(用户矩阵)——扩展为四个潜在特征**

![](img/6393dfbc37186ebf39f7141cfddec869.png)

Users Matrix — P

**QT(乘积矩阵转置— Q) —扩展为四个潜在因子**

![](img/e190df5deb41bedff9eb4ee2620163cd.png)

Product Matrix Transpose — QT

这是一个纯数学练习，其中我们知道 matrix-R 的值(并非所有评级都是已知的)。我们首先用随机值初始化用户矩阵和乘积矩阵。

用户 u4 对产品 P2 (u4P2)的评级是两个向量的乘积——用户(U4)和产品(p2)。

u4p 2 = u41 . p21+u42 . p22+u43 . p23+u44 . p24

如果我们注意到上面的等式——特定用户对任何产品的偏好与两个向量的不同维度的系数之和成正比。

让我们再来看看矩阵分解方程

R = P x Q

这里 P 和 Q 都是未知的。只有几个 R(用户评价产品)值的系数是已知的。

当 P 和 Q 都是变量时，R 有多个解对(P，Q)。

u4p 2 = u41 . p21+u42 . p22+u43 . p23+u44 . p24

原始矩阵 R —

![](img/e6a23bdc0ad342ad80bfa4ffe2308b0f.png)

Original Rating Matrix — R

高亮显示的单元格是没有被用户评级的单元格。它们变成了测试细胞。

不发光的单元格是我们已经知道产品等级的地方。

我尝试了多次迭代求解 P 和 Q 矩阵的值，每次都得到不同的结果 Q。

迭代 1:

![](img/e9703ffe0e04e867fa8c2f0cac330d36.png)

Predicted rating Matrix — X after iteration-1

![](img/7b37715f1836e39358ae3e2ae5e75ed8.png)

Users Matrix — P after iteration 1

![](img/aca91dc9ae31877630c3e5c60526aca3.png)

Product Matrix Q after iteration 1

X —用户产品评级的预测值(R 是原始矩阵)

P —分解后的用户矩阵

Q —分解后的乘积矩阵

**迭代 2:迭代 2 的输出**

![](img/c90b93a431d82688521f95505507647b.png)

Matrices after iteration 2

**迭代 3:迭代 3 的输出**

![](img/891593bd984f661dd2361de430ffa336.png)

Matrices after iteration 3

**迭代 4:迭代 4 的输出**

![](img/9d68abc7a519b7a6f23d6a0be1b7a512.png)

Matrices after iteration 4

简而言之，我们有 8x4 + 4x4 = 48 个变量，但不到 32 个方程。很明显，我们会有多对 P 和 Q 矩阵。

除了解释 k1，k2，k3，k4 意味着什么之外，这是为了得到 P 和 Q 的一致值而进行的斗争？除非我们在获得 P 和 Q 的收敛值时具有一致性，否则我们对未评级产品的预测将继续波动。

**当前模型的问题—**

去因子分析有助于我们理解——我们如何预测尚未评价/或使用某些产品的其他用户的偏好。基于预测的偏好，我们可以决定更好销售的营销策略(交叉销售和追加销售)。

1.潜在因素的数量是未知的

2.每次迭代都会给出不同的用户矩阵和产品矩阵——这意味着预测不一致

3.潜在的因素是未知的——这就产生了一个使模型具有规定性的问题。这意味着——假设我们要推出一款新产品，但我们不确定——我们应该更多地关注哪些功能以获得更好的销售。

**解决方案-**

当我们只有一个等式 R = P x Q 时，解决这个问题的一种方法是固定变量 Q(产品特性)，这样我们就只需要处理一个变量(P —用户特性)。

凭经验思考——这是个不错的选择。如果我们在销售某些产品，我们最好知道产品的特性是什么，以及我们有多少关键特性。

让我们理解固定 K 的值和矩阵 Q 将如何帮助获得 P 的一致结果和 r 值的收敛预测。

当我们分析上述等式时

产品等级(u4p 2)= u41 . p21+u42 . p22+u43 . p23+u44 . p24

用户特征向量— u4 = u41.i + u42.j + u43.k + u44.t

产品特征向量— p2 = p21.i + p22.j + p23.k + p24.t

其中 I，j，k，t 是向量的四个不同维度。每个维度对应一个独特的特征。

当我们将 Q 值固定为–

![](img/f9f76eb8ea864fd33035959d2e446297.png)

Product Matrix Q (fixed one)

我们开始在 P 值和等级(X)的预测值以及用户矩阵-P-中获得一致性

迭代 1:

![](img/83730942e31aa9935c475fc38811f59b.png)

Rating Matrix X and User Matrix P after iteration 1

用户矩阵(P)开始收敛。请查看迭代 2、3 和 4 的值。

迭代 2:

![](img/b2f14a50e4731ad138001dfd3c2dde68.png)

Matrices after iteration 2

迭代 3:

![](img/877c734b3919652aa0b8c8b17fa34e9c.png)

Matrices after iteration 3

迭代 4:

![](img/6c5620abab9ddee5cbdaf30b34ec42d8.png)

Matrices after iteration 4

基于上述数据，我们可以确定代表用户偏好的用户特征向量。

**现在关键问题仍然是——如何修正产品矩阵？**

**选项 1:**

特征的数量——K——必须根据对产品特征的理解来估计。

产品矩阵的系数值—范围从 0 到 1 (0 表示功能对产品没有任何影响，1 表示功能对产品影响最大)。

一旦我们知道了什么特性(k1，k2，…Kn)意味着，我们可以根据它们对产品质量的贡献来分配从 0 到 1 的系数。

业务 SME 和技术团队都需要一起工作来确定初始关键特征和确定系数的权重。

**选项 2:**

特征的数量——K——必须根据对产品特征的理解来估计(类似于选项 1)。

现在分解矩阵 R，并在几次迭代中确定矩阵 P 和 Q。根据 Q 值的两次迭代和对产品特性的理解做出最佳猜测。

固定 Q 的值并求解矩阵 P。一旦矩阵 Q 固定，矩阵 P 的系数将收敛。

事实上，确定 K 值和乘积系数是很好的方法。这样，我们可以计算用户矩阵的等效系数。

比方说，我们决定根据 5 个关键特征对产品进行分类，并确定每个系数在整体产品偏好中的重要性，这将有助于确定用户矩阵中的相关特征，其中哪个系数对应于哪个特征也是已知的。

**关键步骤总结—**

1.假设 K —基于对产品特性的理解

2.从 P 和 Q 系数的随机值开始

3.迭代并确定第一组 P 和 Q 值

4.查看 Q 系数—尝试将 Q 与产品特性联系起来(产品/项目特性应该是已知的)

5.固定 Q 值和关键特征数量(K —潜在因素)

6.调整 Q 矩阵(产品特性)

7.使用 Q 的调整值来确定 P 的值

**需要牢记的关键事项—**

我忽略了用户对产品评分的偏见(只是为了让计算更简单)。

产品特征与个体维度相对应。尺寸相互垂直。特征向量中不应该有共线性。

当我们确定产品特征时，假设 k1、k2、k3、k4…我们可以根据系数的相对值解释不同潜在因素的初始含义(较高的主导特征将具有较高的系数)。

用户特征将对应于同一组产品特征。假设如果产品 k1 代表产品安全特征，用户 k1 将指示用户对安全的偏好。

**结论—**

最近我在看谷歌 CEO(桑德尔·皮帅)在谷歌 2018 I/O 上的演讲，他谈到了基于眼睛扫描图像预测心血管事件。

许多过去事件(病史、环境、习惯、药物等)的影响将会影响许多其他事件(健康状况——心血管事件)和眼睛内部。

过去发生了一系列事件。现在，他们正在影响心脏骤停的几率以及眼睛内部。

通过测量眼部扫描的变化/情况，我们可以关联心脏骤停的可能性。

![](img/8b1a06892e266a0e05cef4fd6afc80d1.png)

Understanding common factors which impact heart and Eyes conditions

类似地，我们可以找到许多其他用途——疾病相关性与不同位置的水质。

上述关系，我们也可以根据深度学习中的神经网络层进行映射。

实体 1 (E) —不同类型的扫描眼睛图像

实体 2 (H) —不同类型的心脏疾病

潜在因素——不同组的活动、既往病史、人口统计学等是特征向量。它们在深度学习模型中充当输入。我们可以收集病人的各种数据记录——眼睛扫描和心脏状况。使用矩阵分解——我们可以确定两个实体之间的相关性。

![](img/2be0d7825d7a565b43c1768e86217762.png)

Representation in neural network term

我最近了解到——前列腺癌在东部非常普遍。我们只需要收集不同地点与该地区流行疾病的数据，了解可能的潜在因素，并深入处方医学。这在人口健康管理(ACO)的背景下非常有用。

同样，我们可以研究水质、空气质量、工业存在、污染水平、土壤质量对不同地理区域各种疾病的影响。

**受众—** 实施数据科学项目需要业务团队和技术团队(数据工程和数据科学团队)的协作。数据科学组开发算法来为数据建模并评估性能，而业务组帮助理解产品功能并收集建模所需的相关数据。

在初始化用户和产品矩阵时，利用业务 SME 的经验来理解产品特性的相关性、将它们放入正确的序列、分配正确的权重将是至关重要的。因此，两个团队需要紧密合作来创建健壮的/规范的系统。

**参考文献—**

【https://www.youtube.com/watch?v=MSpF84kevyU 

[http://www . quux labs . com/blog/2010/09/matrix-factorization-a-simple-tutorial-and-implementation-in-python/](http://www.quuxlabs.com/blog/2010/09/matrix-factorization-a-simple-tutorial-and-implementation-in-python/)

[https://en . Wikipedia . org/wiki/Matrix _ factorization _(recommender _ systems)](https://en.wikipedia.org/wiki/Matrix_factorization_(recommender_systems))

[https://www.youtube.com/watch?v=XkY2DOUCWMU&list = plzhqobowt qd D3 mizm 2 xvfitgf 8 he _ ab&index = 5&t = 0s](https://www.youtube.com/watch?v=XkY2DOUCWMU&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&index=5&t=0s)

[http://infolab.stanford.edu/~ullman/mmds/ch9.pdf](http://infolab.stanford.edu/~ullman/mmds/ch9.pdf)