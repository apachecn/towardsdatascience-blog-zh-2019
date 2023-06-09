# 排气数据在数据科学中的重要性

> 原文：<https://towardsdatascience.com/importance-of-exhaust-data-in-data-science-2f5c1ab5df03?source=collection_archive---------28----------------------->

![](img/114a30e793d8254f31f0c38d619c4965.png)

Image Credit: NASA/JPL-Caltech

当我第一次听到排气数据这个术语时，我被迷住了。关于同一个主题有很多不同的定义，我想深入探讨一下。简而言之，耗尽型数据是在没有特定目的的情况下生成的数据，可能不会立即显示出对组织在管理、存储和使用这些数据上花费金钱的重要性。嗯，让我们再举几个例子，同时我们会尝试将这些例子与数据科学联系起来。

几个例子(我们这里只是触及冰山一角！):

**网购活动:**假设你去一家网店买鞋。你看了几十个，最后选了一个放在购物车里。一个小时后你回来了，最后买下了它。对于在线商店，主要信息是您点击了哪双鞋，您将哪双鞋放在购物车上，您的鞋码，以及最终的交易信息。现在，让我们考虑一下尾气数据。这可能是你的位置信息，你在其他产品上花费的时间，你搜索的短语，鞋子在购物车中的时间，你使用的设备，安全日志，cookies 等。利用这些废气数据，您可以使用数据科学获得一些可行的见解，如产品推荐、欺诈检测、高效营销、改善客户体验、价格优化等。

**有人发微博吗？:**假设有人发微博说“第一场雪就像初恋——劳拉·比尤斯。”仅仅这条推文和用户名可能不会给我们太多的见解。以元数据的形式用尽数据，比如位置、设备 id、发布时间、用户的关注者数量、用户关注的用户数量、帐户的创建日期等等。现在，零售商店可以使用这些数据来储备药品、供应品、冬靴，媒体流媒体公司可以使用这些数据来播放假日电影，紧急服务可以使用这些数据，导航服务可以提醒司机等等。

**视频:**这是一个非常有趣的空间。视频自然带有一些元数据，如时长、文件大小、格式、创作者/导演、演员等。然而，数据科学在这方面的范围相当有限。进入机器学习，我们可以根据声音、场景的情感(想想静止图像上的情感，因为视频只是一系列超快的静止图像)、场景的位置、历史重要性、成人内容识别来自动生成文本。自然，这些元数据大量用于个性化视频分段、内容审核、视频推荐、基于内容的搜索和索引视频、个性化广告制作、成人内容过滤等。

**物联网空间:**同样，这是一个非常广泛的话题，与其他例子类似，工业物联网中的尾气数据可能是最大的。例如，世界上最大的金属和矿业公司之一 Rio Tinto 每分钟产生 2.4 万亿字节的数据，而地震数据的总量可达数十亿字节[1]。我觉得这里有两件事改变了游戏规则。得益于云计算，存储和计算的成本在过去十年中以指数速度下降。2.边缘计算尺寸减小，功耗增加(例如 FPGAs)。由于这种技术进步，这些公司可以在本地边缘运行机器学习模型，并保持存储大量数据以进行历史分析。

当然，这些只是收集尾气数据的热情日益高涨的几个例子。在这个蓬勃发展的信息社会中，每个工业部门都在利用尾气数据的力量来获得竞争优势，并在客户满意度方面出类拔萃。

总之，虽然收集尾气数据提供了一个很好的机会，但它也带来了保护个人和敏感信息的责任。一个例子是国家安全局大规模收集电话记录[2]。两名斯坦福大学的研究生在他们的研究中发现，监控元数据可以用来查找呼叫者的信息、医疗状况、财务和法律关系[3]。本着开放、积极和道德的心态，我认为利用尾气数据的领域将在未来成为游戏规则的改变者。

# 参考

[1]

G.Goidel，“https://rctom.hbs.org”，2018 年 11 月 12 日。【在线】。可用:[https://rctom . HBS . org/submission/data-is-the-new-oil-Rio-Tinto-builds-new-intelligent-mine/。](https://rctom.hbs.org/submission/data-is-the-new-oil-rio-tinto-builds-new-intelligent-mine/.)

[2]

E.中岛，“www.washingtonpost.com”，2015 年 11 月 27 日。【在线】。可用:[https://www . Washington post . com/world/national-security/NSAs-bulk-collection-of-Americans-phone-records-ends-Sunday/2015/11/27/75d c62e 2-9546-11e 5-a2d 6-f 57908580 b1f _ story . html？no redirect = on&UTM _ term = . 2f 344 e 00 EB 33 .](https://www.washingtonpost.com/world/national-security/nsas-bulk-collection-of-americans-phone-records-ends-sunday/2015/11/27/75dc62e2-9546-11e5-a2d6-f57908580b1f_story.html?noredirect=on&utm_term=.2f344e00eb33.)

[3]

C.b .帕克，" news.stanford.edu "，2014 年 3 月 12 日。【在线】。可用:[https://news . Stanford . edu/news/2014/March/NSA-phone-surveillance-031214 . html？UTM _ content = buffer 07d 49&UTM _ medium = social&UTM _ source = Twitter . com&UTM _ campaign = buffer。](https://news.stanford.edu/news/2014/march/nsa-phone-surveillance-031214.html?utm_content=buffer07d49&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer.)