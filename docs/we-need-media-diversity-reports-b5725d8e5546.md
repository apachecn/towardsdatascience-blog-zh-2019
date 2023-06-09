# 新闻媒体中的性别代表性数据

> 原文：<https://towardsdatascience.com/we-need-media-diversity-reports-b5725d8e5546?source=collection_archive---------23----------------------->

## 新闻媒体有女性问题吗？

![](img/8416b8bef81d047e44e6c0f10dd7ef43.png)

在科技多样性的问题上，已经有了很多的笔墨。例如，来自脸书和 T2 的谷歌刚刚发布的多样性报告显示，这些公司的男性数量是女性的 2 倍。这些统计数据在[卫报](https://www.theguardian.com/news/datablog/ng-interactive/2014/nov/25/diversity-in-tech-gender-breakdown-of-key-companies)、 [NBC](https://www.nbcnews.com/news/asian-america/report-finds-little-change-tech-industry-leadership-diversity-n824926) 、 [Vox](https://www.vox.com/recode/2019/6/17/18678541/women-tech-photoshop-diversity) 、 [CNN](https://www.cnn.com/2019/03/05/success/diversity-fatigue-resistance/index.html) 和[许多](https://money.cnn.com/interactive/technology/tech-diversity-data/) [其他](https://techcrunch.com/2019/06/17/the-future-of-diversity-and-inclusion-in-tech/) [新闻](https://www.cnbc.com/2018/06/20/silicon-valleys-diversity-problem-is-its-achilles-heel.html)网站上引发了负面评论。

![](img/763a4d32b977f54c302f82d51fc8e10f.png)

screencap from Google’s 2019 Diversity report

指责科技巨头很容易，但我发现，如果媒体公司照照镜子，他们会发现自己有许多同样的问题。在过去的 6 个月里，我从 15 个不同新闻机构的主页上收集了数万篇文章。通过分析这些文章的作者，很明显大多数新闻作者是男性。似乎就像科技行业一样，新闻媒体是男性主导的，需要改变。

# 方法学

对于感兴趣的人，我想快速解释一下这些数据是如何收集和分析的。通过这样做，我希望表明，虽然有些地方可能会有误差，但它们应该基本上不相关，偏差最小。此外，与这个项目相关的所有代码和数据都在 github [这里](https://github.com/taubergm/GenderInTheNews)。

## 数据收集

2019 年每天使用 python [NewsScraper 库](https://newspaper.readthedocs.io)从多个新闻网站收集新闻数据。使用这个工具，我将多个网站的头版新闻保存到一个大数据库中。虽然我不能保证每个故事都被保存下来，但我确实得到了一个大样本，其中大部分是随机选取的。

一旦故事进入数据库，就有可能检查新闻文章的作者。不幸的是，编写器数据通常包含需要删除的描述性词语(即美联社记者)。我不得不编写脚本来过滤作者姓名，并确保我最终得到的是一个真实的人的列表。此外，许多故事都有多个作者，所以我必须确保这些作者是分开统计的。最终的结果是一个由数千个名字组成的列表，这些名字代表了 2019 年在一个主要新闻网站上发表的任何人。

最后，有了一个已知的好名字的列表，我创建了一个新的数据库，其中存储了作家的名字、他们发表的故事数量、他们的组织以及他们的性别。这最后一部分很棘手。我使用了男性和女性名字的 [python nltk 语料库](http://www.nltk.org/howto/corpus.html)，并补充了我能找到的尽可能多的其他[名字](https://names.mongabay.com/male_names_alpha.htm)样本。如果一个作家的名字出现在一系列“男性”名字中，我会这样标注。如果第一个名字出现在“女性”名字列表中，它们就会被标记为女性。最后，一小部分被标记为“未知”。这可能是最大的错误来源，因为一些名字如“Sam”可以适用于任何性别。尽管如此，我相信大多数错误都是随机的，得到的结果是有效的。

# 结果—全行业

> 不仅新闻作者更有可能是男性，而且男性作家更有可能获得出版。

查看新闻行业性别分类的最简单方法是，看看作家中男性和女性各占多大比例。这个简单分析的结果有些令人震惊。

与科技工作者一样，新闻故事的创作者可能是男性的两倍(除去不知名的名字，男性为 63%，女性为 37%)。

![](img/a4a9a2c4090a04ab3def88a6bca92d07.png)

each block represents 100 news writers

如果我们计算新闻 ***文章*** 的数量而不是新闻 ***作者*** 的数量，情况就更糟了。这表明，不仅作家更有可能是男性，而且男性作家更有可能获得出版。

![](img/b2d32d653202cb7481fd35737c3e6005.png)

each block represents 1000 news stories

除去“未知”性别作者的文章，我发现男性大约占 71%,女性仅占 29%。

# 按新闻网站列出的结果

> 正如我们所料，自由主义新闻来源似乎比保守主义新闻来源有更好的性别平衡。

## 作家

之前的分析包括了所有的新闻来源。这些网站存在于不同的政治领域，所以我们可以预期它们的性别平衡会有所不同。下面我画出了每个媒体渠道的作家分布。底部的图删除了名字不容易映射到性别(即“未知”性别)的作者。

![](img/2d480c3133caa95973a349fb4c338ab1.png)![](img/5d625c051dcb714ee6f65ac77d955157.png)

正如我们所料，自由主义新闻来源似乎比保守主义新闻来源有更好的性别平衡。像 NPR 和 CNN 这样的网站，男女作家的比例几乎是 55:45。《纽约时报》、《卫报》、《波士顿环球报》和《洛杉矶时报》等老牌报纸的比例接近 65:35。在政治光谱的右端，像福克斯新闻频道、每日来电和布莱巴特这样的网站都有超过 70%的男性作者。这相当极端，即使考虑到保守派更有可能是男性。

## 文章

> 正式作家的性别平衡可能比很少投稿的客座作家好得多。

看看故事的性别分类，而不是作家，类似的模式出现了。

![](img/ded2cbc73999d130a9cd31421a46fa1d.png)![](img/2a3188b6d3b7afeae218bcaac2acf23b.png)

有趣的是，某些新闻机构的情况有所改善。我怀疑正式作家中的性别平衡可能比很少投稿的客座作家要好得多。

根据这一新标准，《华盛顿邮报》的男女比例接近 50:50，《华尔街日报》的男女比例接近 60:40。尽管如此，总体而言，性别平等的情况并不乐观。此外，如果新闻媒体真的喜欢男作家的客串特写，这仍然是一件值得思考的事情。

# 最后的想法

正如技术的多样性对于创造一个更加公正的社会至关重要，媒体的多样性也是如此。科技巨头们终于意识到了他们的社会责任。在过去的几年里，他们对员工的多样性保持透明，并发布年度报告显示他们的进步。鉴于他们拥有巨大的文化和政治影响力，我认为现在是新闻机构做同样事情的时候了。

我收集的数据无疑有缺陷。不幸的是，没有真正的多样性报告，这是我们目前能做的最好的。如果这些发现是准确的，那么新闻媒体在实现它经常宣扬的那种平等之前还有一段路要走。