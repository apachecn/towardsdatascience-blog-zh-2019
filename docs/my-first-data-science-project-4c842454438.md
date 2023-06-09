# 我的第一个数据科学项目

> 原文：<https://towardsdatascience.com/my-first-data-science-project-4c842454438?source=collection_archive---------33----------------------->

# 我为什么要写这篇文章

作为一个在数据科学领域工作了一段时间的人，我收到了不少热情的毕业生的问题，他们问我“如何成为一名数据科学家”或“数据科学家每天都做些什么”。另一方面，我偶尔听到一些声音开玩笑说“[数据科学家是 21 世纪最性感的工作](https://hbr.org/2012/10/data-scientist-the-sexiest-job-of-the-21st-century)”不再是真的了:大多数数据科学家的时间可能会花在繁琐的任务上，如运行 SQL 来提取数据，构建仪表板来做报告，以及(更令人沮丧的)你需要维护它们！他们问我作为一名数据科学家的经历是什么，我对这一现象有什么感觉，以及在最初的声明发表 7 年后，数据科学是否仍然“性感”。许多类似的问题都围绕着这个主题，我认为通过一个关于我的第一个数据科学项目的故事来分享我的个人观点可能会有所帮助。这可以作为一个参考点，希望它也可以激励那些仍然渴望加入该领域的人，或者那些刚刚开始他们的第一份数据科学工作的人，甚至那些已经在该领域工作了很长时间的人。

![](img/33c18e20bed57bef132e40a6c221f081.png)

注意。这不是我作为数据科学家的第一个实际项目，正如你所知道的，开始任何工作，都需要在开始时做一些琐碎的任务，以了解基本知识。这个项目是我 2013 年在 TrueCar，Inc .开始数据科学职业生涯后的第三个月做的。

# 故事

研究生毕业后，我加入了 TrueCar，开始了我的第一份数据科学家工作。对于那些不知道的人来说，TrueCar 是一个在线购车平台，它提供透明的定价信息(例如，最近的车辆交易价格)，因此客户不会为一辆车多付钱。当时，作为一名应届毕业生，我对数据科学团队正在从事的所有项目非常着迷，这些项目几乎涵盖了一家以数据为中心的技术公司运营的所有业务方面:构建定价模型以支持核心产品，用 A/B 测试优化网站等。在第一个两个月的入职期后，我被分配到搜索引擎营销领域工作。

搜索引擎营销(SEM)是搜索引擎巨头，如谷歌，发明的游戏。这个游戏的一个过于简化的观点是:公司决定关键词的竞价价格(例如，“新丰田卡罗拉”是一个 3 个单词长的关键词)。如果用户搜索准确的关键词，并且该公司的出价高于其他竞争对手，它将赢得该位置，并可以将他们的产品信息放在用户将看到的所有搜索结果的顶部。如果用户点击产品链接，该公司就会向搜索引擎巨头付费，通常是第二高的出价。几年来，TrueCar 一直在使用 SEM 来帮助获取客户，系统中已经有成千上万的关键字需要维护，这些关键字是由不同的活动组织的。我分配的项目是报告每个 SEM 活动的表现，并使用 Google 的 AdWords API 自动报告。

![](img/bf6a2f8ebf8aab731c4f065ecb5945eb.png)

我对这个项目非常满意，它是我练习 Python 技能和学习更多 AdWords API 的一种方式，尽管这看起来一点也不“性感”。反正我就开始摆弄 Adwords，写点代码，很快就收集了很多关键词性能数据然后用它们编了一个报告。

# 有点好奇

在生成第一份活动绩效报告后，我发现“每次转化成本”(CPC)是人们都关心的指标；这并不奇怪，因为这个指标意味着我们为一个转化的客户支付多少钱:越低越好。我还做了一些关于 SEM 行业的研究，并意识到“关键词”是搜索引擎营销的一个重要方面:它们并不平等，两个关键词在“每次转换成本”方面可能有显著不同的表现。当时，我想到了两个问题:1 .哪些关键词性能更好(CPC 更低)？2.我们是否已经在系统中拥有了所有性能更好的关键词？

# 一些科学，一些算法

手动浏览系统中的所有关键字以获得任何有意义的见解是不可能的，想象一下可能有类似“我真的想买一辆现代索纳塔”的关键字(是的，我刚刚在谷歌中进行了搜索，所以它是其他公司可以竞标的关键字，并且它至少有一个搜索流量)。所以我需要更有策略，在流程中加入一些“科学”成分。我开发的算法或过程如下:

*   第一步。对于所有活动中的每个现有关键词，生成 1 克和 2 克的子关键词。例如，“新丰田卡罗拉”关键字将生成以下 5 个子关键字:“新”、“丰田”、“卡罗拉”、“新丰田”、“丰田卡罗拉”
*   第二步。为每个子关键字分配性能，就好像它们是关键字本身一样。例如，如果“新丰田卡罗拉”有 100 美元的 SEM 支出，导致 10 次点击和 2 次转化；那么所有 5 个子关键词都将具有相同的表现。
*   第三步。按所有子关键词分组，并计算它们各自的成本和转化率，然后我们就可以得到它们的平均每次点击费用，以点击数作为相对大小的参考
*   第四步。按照点击费的表现对所有子关键词进行排序，较低的点击费排在最上面

![](img/1622b88b49a37262c6ba0285f525d62e.png)

这肯定不是最好的算法:有相当多的子关键词完全没有任何意义，比如“购买 a”、“the”等。但是，也有一些有趣的子关键词出现在列表的顶部:其中之一是“最佳价格”。这个子关键词的点击费低得惊人，但只有几百次点击。嗯…，这是什么意思？

# 貌似合理的商业解释

为什么“最优价格”表现更好？融入一些商业知识，一切开始变得有意义:在 TrueCar 上转换良好的人通常有强烈的“找到一笔好交易”的意图，“最佳价格”是在搜索查询中表达他们兴趣的常见方式。从这个角度来看，与“最佳价格”相关的关键词具有较低的 CPC 是有意义的，因为它们的转化意愿(例如，使用 TrueCar 产品)较高。另一方面，我的分析显示，我们只收到有限的点击，由很少的关键字贡献，这表明有机会进一步扩大！

不久，我用几张幻灯片总结了这一发现，以展示这颗“隐藏的宝石”。人们对我的发现有点怀疑，因为特定关键字的样本非常有限，然而，没有人想拒绝用一半的成本获得更多销售的机会，所以我得到了一个绿灯来测试这个想法！为了避免不必要的技术术语和细节，简而言之，我围绕“最佳价格”创建了一组关键词，将所有内容上传到 AdWords，并开始了新的活动。一周后，它收到了大量的点击量，而每次点击费用却大大降低了，每个人都非常高兴。之后，纯粹是执行:通过各种方式产生更多基于“最佳价格”的关键词，我们扩大了多个活动的规模，它们都表现一致:每次点击费用比同行活动低得多。这为公司带来了大量的廉价转换，幸运的是，我的第一个数据科学项目有了一个美好的结局:)

# 回首

很快，在过去的 6 年里，许多事情都发生了变化。如今，SEM 行业更加智能化，大多数关键字选择都通过各种工具实现了自动化。就在今天，当我搜索“价格最优的丰田卡罗拉”时，有四个返回的 SEM 结果，而 TrueCar 不在其中。所以我知道我对这个特定关键词的洞察力已经过时了。在数据科学方面，这个项目不能被认为是辉煌的:算法是初步的(简单的 n-gram 特征提取)，统计数据缺乏一些严谨性(计算 CPC 置信区间的一种非常简单的方法)，工程过程相当粗糙(肯定不是我最好的 Python 代码)。然而，我仍然为这个项目感到自豪，因为它让我尝到了数据的价值；作为一名数据科学家，我可以打开它并享受成功。

# 我对数据科学的思考

现在，您已经了解了我的第一个数据科学项目故事。当然，这只是作为一名数据科学家的成千上万种开始方式中的一种。希望这个故事揭示了“数据科学家”应该具备的三个要素(我认为):

1.  良好的数据分析和工程技能:没有这些，你可能会陷入许多步骤(例如，提取 n-gram，自动启动 SEM 活动等)
2.  合理的商业意识:数据有助于揭示隐藏的商业知识，所以你最好先了解一些基础知识。
3.  (最重要的)你的好奇心:这是让你开心的东西，可以将“繁琐”的任务转化为有趣的项目

![](img/345e6acd3792b998f4069df81e1df944.png)

作为故事的结尾，我想引用我之前关于“数据科学家”的说法:这是大约五年前我的(当时的)数据科学团队接受当地一家报纸采访时所说的话([链接](https://www.builtinla.com/2014/09/03/data-science-101-what-data-scientist-does-and-how-become-one))，我认为这句话现在仍然适用。

*“成为一名数据科学家需要统计学、编程和商业意识的结合。“能够从数据中探索洞察(通过编程&统计)以满足公司业务需求的是‘科学家’。”*

*感谢您的阅读，并随时与那些可能觉得有用的人分享这个故事。文章首发于 LinkedIn([https://www . LinkedIn . com/pulse/my-first-data-science-project-pan-Wu](https://www.linkedin.com/pulse/my-first-data-science-project-pan-wu))，转载于 Medium。