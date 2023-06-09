# 数据可视化竞赛:Tableau 的魔力是什么？

> 原文：<https://towardsdatascience.com/the-race-for-data-visualization-what-is-tableaus-magic-fb5ad92150c5?source=collection_archive---------8----------------------->

![](img/8b2aa06a6319389f8b807a071cfda550.png)

比赛刚刚升温。6 月 6 日，谷歌宣布他们将收购数据查询和探索工具 Looker。考虑到 Looker 与谷歌的数据工作室有些重叠，这是一笔有趣的收购。(然而，当我回想起谷歌下一次发布会时，我不记得有一次提到 Data Studio。)收购 Looker 的目的当然是为了缩小谷歌云在大数据和商业分析解决方案市场上落后于亚马逊网络服务和微软的差距。根据 IDC 的数据，这个市场到 2022 年可能达到 2600 亿美元。

尽管这对谷歌来说是一个重大举措，但更大的消息来自 Salesforce，他们宣布计划以 157 亿美元收购 Tableau！这对 Salesforce 意味着什么？我有两个想法。

首先，Tableau 将极大地扩大 Salesforce 的客户群。Tableau 与 Salesforce 平台和 Einstein 等技术非常契合，提供了更易于使用的企业标准可视化工具。这就是为什么以前不是 Salesforce 客户的许多人和公司现在会成为 Salesforce 客户的一个原因，首先是现有的 Tableau 用户，他们可能会将 sales force 带入他们的技术武器库。小公司、独立承包商或只是数据可视化爱好者将很快成为 Salesforce 每月经常性收入的一部分。(虽然，并不是所有的 Tableau 客户都满意。虽然 Salesforce 承诺保持 Tableau 的多平台方法和对多个数据集的连接，但许多现有的 Tableau 用户需要被说服。毕竟，他们是与 Salesforce 目前的用户群完全不同的用户群。)

![](img/7a69574bede66ca9e75adc882429efe5.png)

其次，这使 Salesforce 更接近与谷歌和微软竞争。这两家科技巨头已经分别提供了数据探索工具 Data Studio(和 Looker)和 Power BI。虽然这些软件解决方案很好，但我不认为有人会说它们与 Tableau 处于同一水平。事实上，画面似乎有某种魔力。人们不仅喜欢使用它，当他们谈论它时，他们真的很兴奋。没有多少应用程序可以这么说。那么为什么 Tableau 会出现这种情况呢？

# 完美的平衡

现在是完全不同的东西，Python。Python 在过去十年中经历了飞速发展。它已经从一些人认为的玩具语言变成了不仅仅是计算机科学家的通用语言，而是所有科学家的通用语言。无论你是天文学家还是化学家，如果你编程，很可能是用 Python。许多人将这一成功归功于 Python 简单而强大的平衡。Python 中的 Hello world 是一个简单的 liner，print(“Hello World”)。这在 Java 中需要三行，在 C 中需要六行(取决于您如何格式化代码)。伴随着编码的简易性而来的还有不错的处理速度。没错，Python 没有 Fortran 快，但是对于一个从 Excel 走过来的人来说，就是闪电了。

Tableau 似乎也发现了这个“恰到好处”的金发女孩地带。它为探索数据提供了高度的可修复性，学习曲线非常平缓。数据可视化的守护神爱德华·塔夫特对此做了很好的总结。“卓越的图形是在最短的时间内给浏览者提供最多的想法…”。

这似乎是 Tableau 的核心设计理念。使用户能够在尽可能少的培训下快速浏览数据。当然，随之而来的是权衡。Tableau 能像 R 的 ggplot2 包一样可定制吗，不能。它能像 D3.js 一样无缝集成到网页中吗，不能。但是与其他两个相比，Tableau 的学习曲线要容易得多。你可以和一个从未使用过 Tableau 的人坐下来，几分钟后他们就会自己去试验和探索数据。Tableau 融合了这些选项的一些最佳特性。它利用了 ggplot 使用的图形语法，并结合了 D3 的交互特性。是的，您失去了一些灵活性，但是在大多数情况下，您获得的速度是值得的。

# 美丽很难获得

任何试图从零开始设计图表或图形的人都很清楚需要选择的因素的数量。有颜色、背景色、刻度线、线条不透明度、比例、字体大小等。这是一项艰巨的任务。最终你会在编辑过程中的某一点，你甚至不确定这是否是一个积极的改变。如果你想知道选择颜色有多难，看看这个 YouTube [关于 matplotlib 重新设计默认颜色图的过程。](https://www.youtube.com/watch?v=xAoljeRJ3lU)

幸运的是，Tableau 为你做了设计选择的重担，10 次有 9 次，它看起来很棒。我问一个同事为什么喜欢 Tableau，他说“它让你的数据看起来很漂亮，你甚至不用去尝试”。*蛮*的价值不可小觑。

在星盘中，美丽通常是没有干扰。如果颜色不对，或者有太多的刻度线，这会分散观众对数据信息的注意力。弗洛伦斯·南丁格尔有一个很好的例子。她使用了一个简单的极区图，使观众的注意力集中在数据讲述的故事上(这里有一个 Tableau 工作簿的链接，一些人复制了南丁格尔的著名图表)。

![](img/40bd0d2b68e47d4adc65ba5b6ab52416.png)

可悲的是，其他可视化工具在这一领域仍然落后。

Tableau 的这种开箱即用的美感，结合其平衡的用户易用性，使其成为数据探索和可视化的事实上的工具。Tableau 的用户遍布各行各业，涉及各种工作职能。事实上，可能唯一比 Tableau 更普遍的数据工具就是 Excel 了。

# 舞台颂歌

我一直很喜欢 Tableau。这是一个很棒的产品，提供了很好的服务。当我听到他们被收购的消息时，我的第一想法是我为他们感到高兴。就好像我听说一个老朋友找到了一份好工作。我仍然记得我的第一本 Tableau 练习册。我在硕士项目的训练营做的。它着眼于 IMDb 的电影评论与烂番茄的电影评论有何不同(这个话题我会再次提及)。从那以后，我可能已经做了一百多个 Tableau 练习册。我用得太多了，已经开始影响到我女儿了。有一次我在家工作，她来到我的办公室，给我看了一张她用彩色笔手绘的图表。这是一个条形图，显示了她有多爱不同的动物，第一是猫。我把它拿过来，用 Tableau 重新制作，让她看看她的作品有多好。

![](img/027fc3719292a330bd436e21d09660bd.png)

Tableau 对我建立投资组合也很重要。甚至我以静态图像结束的数据可视化也是从我通过 Tableau 工作簿探索数据开始的。无论是展示我在研究生院写了多少[行代码](https://medium.com/@mattyancey/grad-school-measured-in-lines-of-code-fa7162d38c54)，还是展示我在[塔可钟](https://medium.com/@mattyancey/purchase-history-of-2011-2014-72bf8cf1f85a)吃过多少次，Tableau 都是帮助我讲述故事的工具。

我的个人资料上写着“我是一名数据科学家、*数据插画师*和作家”。我可能从像尼古拉斯·费尔顿和蒂芙尼·法兰特·冈萨雷斯这样的艺术家那里找到了灵感，但是是画面帮助我实现了这个中间角色。它给了我一个艺术的出口，也给了我一种将美运用到日常工作中的方式。

祝贺 Salesforce 收购了一家伟大的公司。我希望 Tableau 的下一个阶段只会给使用它的公司和人们带来最好的东西，也给那些第一次发现它的人带来最好的东西。