# 使用 SQL 改进缺失值

> 原文：<https://towardsdatascience.com/using-sql-to-improve-missing-values-d1d14cf69797?source=collection_archive---------23----------------------->

![](img/31b7ef4b067ffe8926fcc34c0b804b8c.png)

Missing data points can sometimes feel like missing jigsaw pieces (photo: author)

几个月来，我们一直在研究在数据科学中使用 SQL 的不同方式——最近一次是在[中使用 SQL 检测异常值](/using-sql-to-detect-outliers-aff676bb2c1a)(与检测异常不同，尽管那是将来的事情)。

在这个零星系列的第一篇文章中，我们看到了如何通过计算一列中空值的比例来评估缺失数据。然而，简单地查找和计算丢失的数据点用处有限——如果您找到这些丢失的数据点，您需要有工具可以使用。

所有数据科学家都应该熟悉处理缺失值的核心方法，这句话的意思是“如果你不熟悉，你应该记住下面的列表”:

1.  列表式删除:如果一个变量丢失了太多的事例，以至于看起来毫无用处，那就删除它。
2.  逐例删除:如果某个特定的观察结果缺少太多因素，则将其删除。
3.  虚拟变量调整:如果变量在特定情况下缺失，使用一个假设值代替它。根据问题的不同，中间值可能是直观的选择或代表“中性”设置的值。
4.  插补:使用一种算法来填充值，从最基本端的简单随机数到更复杂端的由自己的模型插补的值。

很明显，SQL 在其中一些方面比其他方面更好。列表式删除就像在 SELECT 语句中去掉列名一样简单；逐例删除可能像 WHERE 子句测试空值一样简单。

使用这两种方法会带来风险——如果数据不是完全随机缺失的，您很容易引入偏差。不难想到由于数据中反映的特定情况而没有收集度量的情况。Frank Harrell 在他的书《回归建模策略》中给出的一个例子是血压测量，这些测量并不针对预期不久就会死亡的患者——因此排除了患者观察值。在患者结果模型中遗漏的血压测量值可能会选择性地排除已经死亡的患者，从而造成明显的偏差。

虽然上面的例子说明了按病例删除的风险，但从同一个例子中也可以看出按列表删除的缺点——如果你忽略所有血压信息，你就忽略了许多对解释医疗结果有用的信息。

一种更复杂的方法是使用 Paul Allison，他是 Sage 系列统计学短评《缺失数据》的作者，他称之为“虚拟变量调整”,其中包括创建一个变量来指示缺失信息的存在。您还需要更新原始变量，以包含一个常数值来代替空值。在 SQL 中，这可能是一个简单的 CASE 语句。我们假设数值常数为 2:

```
SELECT CASE Missing_var WHEN var is null THEN 1 ELSE 0 END, coalesce(var, 2)FROM Table
```

上面的代码是与实现无关的——例如，如果使用 MySQL，您可以用“ifnull”替换“isnull”函数，因为“isnull”是 null 的一个快捷逻辑测试(它可以替换上面的 CASE 语句)，其他实现可能也有类似的快捷方式。

这些处理缺失值的技术是最基本的。虽然公平地说，一些最先进的技术很难在 SQL 中实现，但这些仍然可以在您的旅程中带您走一段合理的距离。

在数据库中使用执行这些步骤的一个原因是，您可以通过延迟选择建模环境(如 R、Python、Rapidminer 等)来将数据准备和探索步骤与建模步骤分离。，直到你有一个稍微准备好的数据集。您甚至可以在多个环境中执行分析以检查结果。

因此，通过使用 SQL“就地”分析数据并做一些基本的数据准备，您可以通过在第一时间转移到建模环境来保持比可能的更高程度的灵活性。

罗伯特·德格拉夫的书《管理你的数据科学项目》[](https://www.amazon.com.au/Managing-Your-Data-Science-Projects-ebook/dp/B07SWV54LR/ref=sr_1_1?crid=1IJIWKNHFBHOY&keywords=robert%20de%20graaf&qid=1561334793&s=gateway&sprefix=robert%20de%2Caps%2C332&sr=8-1&source=post_page---------------------------)**》已经通过出版社出版。**

*[*在 Twitter 上关注罗伯特*](https://twitter.com/RobertdeGraaf2?source=post_page---------------------------)*