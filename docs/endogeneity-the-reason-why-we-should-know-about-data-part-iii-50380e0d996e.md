# 处理第二类内生性

> 原文：<https://towardsdatascience.com/endogeneity-the-reason-why-we-should-know-about-data-part-iii-50380e0d996e?source=collection_archive---------17----------------------->

## 为什么我们应该了解我们的数据

## 处理第二类内生性的文献中的例子

通过[介绍](https://medium.com/@ashutoshnayakkgp/endogeneity-the-reason-why-we-should-know-about-data-part-i-80ec33df66ae)和处理一种“更简单”形式的内生性([第一类](https://medium.com/@ashutoshnayakkgp/endogeneity-the-reason-why-we-should-know-about-data-part-ii-c1487d69aeed?postPublishedType=repub))，这部分探讨了更困难的同时内生性问题。当 Y 引起 X，X 引起 Y 时，同时发生(富者愈富)。

这个问题很难回答。添加工具变量(iv)可能对
2 没有帮助。这是最常见的，也很难诊断(或识别)3。X 是 *i.i.d.* 的标准假设不成立(一月份优惠券数量的影响可能会持续到三月份)。

如果不纠正同时性，错误模型的不良影响和对错误模型的信心仍然对同时性有效(如第二部分*省略变量*所述)。在大多数向客户发放优惠券的公司中，优惠券是根据**某种**策略决定的(这可能是之前的数据科学家构建的模型)。

博客不能涵盖同时性。因此，一些关于在哪里同时阅读的例子。

**例 1。**药品明细:制药公司向医生投放广告。他们在处方量较高的医生身上花费更多。数据科学家可以在模型中使用滞后处方，其中当前处方不仅取决于当前的详细程度，还取决于以前的处方。

**例二。**电影/产品/节目在不同的城市相继上映，这取决于在影院上映的竞争电影以及来自电影先前上映城市的电影评论。因此，在哪里和哪个城市上映电影的决定取决于电影的表现。选择合适的工具变量(或使“*其他事物等于*”)的控制变量，内生性是可以处理的。思路是:驱动前几个城市票房的外生变量会驱动下一个城市的票房。因此，找到正确的 IVs 有助于对抗同时性。在论文中，他们使用竞争电影的指标作为 iv。

**例 3。**一家公司可能会根据 R、F、M 值(非常常用:新近度、频率和货币)向买家发放优惠券。t-1 时的 RFM 可用作控制变量(因为它们与 t 时的误差无关)。也可以考虑控制函数(第二部分)方法，其中 R、F、M 回归为 t-1 时 R、F、M 的函数，R、F、M 的预测值和实际值之间的差异用作销售建模时的独立变量。

**例 4。**在冰淇淋供应商示例中，可以使用价格和 error_i 的联合概率分布，而不是使用温度作为 IV。虽然 IVs 控制方法模型需要数据收集的精确结构，但它并不总是可用的。例 1 中考虑的模型假设了响应模型的知识(X|Y 如何导致 Y ),这也是未知的。Copula 方法是一种使用回归量 X 和 error_i 的联合分布的无模型方法。Copula 是一种将 m 维多元分布耦合到 m 个一维边际的函数。这种方法使用最大似然法来获得联合分布。

我希望这三个部分能让你明白了解数据来源的重要性(数据是如何创建或收集的)。虽然现代机器学习方法能够通过*省略*变量来处理内生性，但是*同时*在建立模型*之前需要一些头脑风暴。*

这些参考资料是:

1.  [内生性的非技术性指南](https://link.springer.com/referenceworkentry/10.1007%2F978-3-319-05542-8_8-1)(博客第一、二部分的基础论文)
2.  [药品详情](https://www.jstor.org/stable/30164711?seq=1#metadata_info_tab_contents):市场研究杂志
3.  [用户评论对电影表现的影响](https://pubsonline.informs.org/doi/abs/10.1287/mksc.1100.0572):市场营销科学
4.  [用 copulas 处理内生性](https://pubsonline.informs.org/doi/abs/10.1287/mksc.1120.0718):营销科学
5.  [税收优惠券](https://pubsonline.informs.org/doi/abs/10.1287/mnsc.2017.2934):管理科学

*原载于 2019 年 6 月 2 日 https://medium.com**的* [*。*](https://medium.com/@ashutoshnayakkgp/endogeneity-the-reason-why-we-should-know-about-data-part-iii-3ac44948b148)