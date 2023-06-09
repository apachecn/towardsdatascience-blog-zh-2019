# 数据越多未必越好

> 原文：<https://towardsdatascience.com/more-data-might-not-be-better-c4db0e03b500?source=collection_archive---------32----------------------->

![](img/f56bd8d4b9147d7c18516f2f8d32b485.png)

Prospecting for Data Insights (Vermont Historical Society)

在大数据高峰期前后的一段时间里，有一句口头禅占据了主导地位:只要能够获得足够的数据，任何问题都可以得到解决。当这句咒语被引用时，它似乎经常隐含着这样的信息:担心你是否拥有正确的数据是恐龙的方式。

尽管对大数据的大肆宣传已经过去，但这一思想的回声仍然存在于 2019 年的数据战略中，这些战略将数据收集置于前沿和中心位置，并将不断增长的数据缓存置于对数据科学家预期要解决的问题的清晰理解和对现有数据的深刻分析之上，以确保这些问题发生。

在许多方面，这些旨在利用物联网宣传的战略与最初围绕数据科学的宣传相反，最初的宣传认为，每个组织都坐在未经分析的数据的金矿上，等待被部署来解决组织的大多数问题。如果这个金矿真的存在，为什么还需要收集更多的数据呢？在第一波数据科学炒作中，缺乏分析数据的熟练人员，但现在有一种说法是[供过于求](http://veekaybee.github.io/2019/02/13/data-science-is-different/)——物联网只是数据科学家的一个工作计划吗？

部分问题可能是对不同机器学习技术的相对有效性缺乏广泛的认识——特别是每种技术需要多少数据才能获得可用的结果。这是由于缺乏对“平坦最大效应”的理解，模型往往会达到一个点，在这个点上，增加的复杂性不再导致增加的准确性:建模者版本的经济学“收益递减规律”。

回到缺乏对不同机器学习算法的方式的认识的问题，这些算法对于它们有效工作所需的数据量有不同的要求。[最近的研究](https://bmcmedresmethodol.biomedcentral.com/articles/10.1186/1471-2288-14-137)证实了预期的结论，即针对较小数据开发的算法(如逻辑回归)可以实现与现代技术(如随机森林)同等的准确性，而训练案例却少得多。

记住，逻辑回归相对来说更适合于提供一个内在可解释的模型，如果您有合适的数据集来获得足够的结果，为什么收集大量不同的数据是一个高优先级？

或者，可能更频繁的是，如果你还没有测试你的数据集是否足以从逻辑回归或类似的方法中得到你需要的结果，你为什么还要讨论你想要收集的其他数据呢？

没有明确目标的数据科学是没有意义的。在我居住的澳大利亚，有一个和[‘banker’](https://www.amazon.com.au/Wunch-Bankers-Hayne-royal-commission-ebook/dp/B07NNN85MW/ref=sr_1_1?crid=5WJ6O7UXHTSA&keywords=wunch+of+bankers&qid=1566193670&s=gateway&sprefix=wunch+of+ban%2Caps%2C295&sr=8-1)押韵的词，用来形容从事这种追求的人。[需要重复](/defining-a-data-science-problem-4cbf15a2a461)的是，对于希望拥有有效数据科学项目的数据科学家和组织来说，投入时间的最重要地方是仔细定义每个数据科学项目的目标。过于关注从所有可能的来源收集大量数据的危险在于，对解决组织真正问题的关注被忽略了。

*罗伯特·德格拉夫的书《管理你的数据科学项目*[](https://www.amazon.com/Managing-Your-Data-Science-Projects/dp/1484249062/ref=pd_rhf_ee_p_img_1?_encoding=UTF8&psc=1&refRID=4X4S14FQEBKHZSDYYMZY)**》已经通过出版社出版。**

*[*在 Twitter 上关注罗伯特*](https://twitter.com/RobertdeGraaf2)*