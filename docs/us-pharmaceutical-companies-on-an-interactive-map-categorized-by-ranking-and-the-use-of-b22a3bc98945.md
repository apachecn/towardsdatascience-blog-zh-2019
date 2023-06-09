# 互动地图上的美国制药公司:通过排名和人工智能(AI)的使用进行分类

> 原文：<https://towardsdatascience.com/us-pharmaceutical-companies-on-an-interactive-map-categorized-by-ranking-and-the-use-of-b22a3bc98945?source=collection_archive---------14----------------------->

![](img/088761635a133b5c480ab26e1d76a13f.png)

# **简介:**

上周，我有机会参加了由美国孟加拉药物科学家协会在马里兰州贝塞斯达举办的会议。在会议上，我与来自制药行业和 FDA 的人交谈。在那些谈话中，我发现大多数在位于该国东海岸的制药公司工作的人，令人惊讶的是，该国有许多我从未听说过的公司。我合理地问自己，“大多数制药公司都位于东海岸吗？或者它们是如何分布在各州的？为什么我没有听说过这些公司的名字”？。在谷歌上快速搜索“美国制药公司”给了我几个链接。其中，这两个(drugs.com 和 rxlist.com)网站很有帮助，到目前为止，drugs.com 包含了更多的信息。所以，我开始用 python 保存所有公司的信息，包括它们在 drugs.com 的地址。

# 数据:

这里是我写的代码的快照，但是为了保持文章简短，我不会在这里分享所有的代码。

这个代码让我想到网站上有 404 家公司。所以，我开始从链接中收集这些公司的地址。大约有 80 个链接是灰色的，我发现它们要么被大公司收购，要么是大公司的一部分。所以，我剩下了大约 320 个链接。在第一次尝试中，我保存了 262 家公司的信息，包括名称、完整地址、网站和职业页面链接。在另一次尝试中，它只给了我一些公司的信息(名称和地址)。然后，我手动添加了一些数据，总共创建了 308 家公司的信息，包括它们在该国的实际地址。

# 第一张地图:

现在，我使用名为“googlegeocoder”的 python 库找到了这 308 个物理地址的纬度和经度。然后，我用 python 的“叶子”库创建了我的第一张地图。现在我想知道，如何在地图上找到顶尖的制药公司？

# 更多数据:

接下来，我在谷歌上搜索顶级制药公司，结果发现 pharmexec.com 是排名前 50 的制药公司的好来源。由于它们被列为图片或带有各自公司的标志，我无法使用我的编码技能。但我还是想回答之前被问到的问题。因此，当我在实验室用脱脂牛奶封闭蛋白质印迹膜时，我不得不手动收集数据。在我对制药公司的信息进行研究期间，我发现相当多的公司将人工智能(AI)用于药物发现，这篇文章题为“33 家制药公司在药物发现中使用人工智能”。这就是为什么我很好奇，想看看地图，看看哪些公司一直在使用人工智能。

这些数据如下所示:

![](img/a8cec042fa31288e4fd10c4d71b61104.png)

# 最终地图:

有了这些数据，我就能制作出我的最终地图了。点击下面的链接查看。

[制药 _ 地图](http://yousufali.net/blog_documents/us_pharma_map.html)

或者在您的浏览器中复制并粘贴以下链接

https://bit.ly/2NWBT7u

你可以放大和缩小左上角的按钮。你也可以用光标拖动和移动页面。

**地图上的颜色是如何工作的？**

如果你点击彩色图标，它会显示公司的名称和一些其他信息，如下图所示。

![](img/87dfc6df8c06833c1bacd4f5c4034b06.png)

*   如果一家公司被列为 50 强并使用人工智能，它将被标记为-红色
*   顶部但不使用人工智能-蓝色
*   不顶但是用 AI-紫色
*   不顶也不用 AI——绿色。

现在，我可以想象你在想什么。你想要资源(代码、数据)还玩它！！所有代码和数据都可以在我的 [github_page](https://github.com/Yousuf28/US_Pharmaceutical_Map) 上找到

感谢阅读。请不要犹豫，在文章下面评论。

最初发表于 [linkedin](https://www.linkedin.com/pulse/interactive-map-pharmaceutical-companies-usa-yousuf-ali/)

# 参考资料:

1.  Drugs.com 制药公司。从 https://www.drugs.com/pharmaceutical-companies.html[取回](https://www.drugs.com/pharmaceutical-companies.html)
2.  克里斯特尔，M. (2019)。pharm Exec 2019 年 50 强企业。从 http://www.pharmexec.com/pharm-execs-top-50-companies-2019[取回](http://www.pharmexec.com/pharm-execs-top-50-companies-2019)
3.  史密斯，S. (2017)。33 家制药公司在药物研发中使用人工智能。检索自[https://blog . bench sci . com/pharma-companies-using-artificial-intelligence-in-drug-discovery](https://blog.benchsci.com/pharma-companies-using-artificial-intelligence-in-drug-discovery)

我的 linkedin

[](https://www.linkedin.com/in/yousuf--ali/) [## Yousuf Ali -研究生研究助理-德州理工大学健康科学中心| LinkedIn

### 孟加拉国达卡 Narayangonj ACI 有限公司产品开发官员。

www.linkedin.com](https://www.linkedin.com/in/yousuf--ali/)