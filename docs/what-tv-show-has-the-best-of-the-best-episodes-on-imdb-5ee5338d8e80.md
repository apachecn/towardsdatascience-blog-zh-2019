# 哪个电视节目有关于 IMDb 的最佳剧集？

> 原文：<https://towardsdatascience.com/what-tv-show-has-the-best-of-the-best-episodes-on-imdb-5ee5338d8e80?source=collection_archive---------9----------------------->

![](img/45b0e0708126f02db9d5a83fa09cd897.png)

## 《绝命毒师》还是《权力的游戏》

“下一集开始于…”

你的大脑还没有处理所有疯狂的情节转折、新披露的信息和人物提升的意义。你刚刚在网飞看了一集令人瞠目结舌的你最喜欢的节目，你被告知下一集几秒钟后开始。

在你知道之前，你已经在推特上说为什么这个节目是世界上最好的东西了。接下来，你在谷歌上搜索那一集来阅读关于它的文章。最后，你去 IMDb，给它打 10 分。

《IMDb 日报》对剧集进行了评级，一些剧集的评级非常突出，因为这些剧集让观众不知所措。对 IMDb 收视率最高的 200 集电视剧进行了分析，以找出在这些令人难以置信的剧集中哪个电视剧制作的剧集最好。

# IMDb 收视率最高的 200 集

信息是从 IMDb 手动收集的，并填入谷歌表格的六个栏目下:电视节目、剧集、流派、评分、年份和投票。这个数据集后来被转换成 csv 文件，用于数据分析。

![](img/bbc2fda771d0ff885c93ec41704749f0.png)

A snapshot of the google sheet file containing the top 200 rated episodes on IMDb

数据可视化用于基于 csv 文件创建多个图形，以显示各列之间的关系。

# 哪一年人们投票最多？

我们制作了一个线形图来显示 IMDb 每年优秀剧集的投票总数。

![](img/82d57b632fdf3bbcc998b623c25790cd.png)

Total Number of Votes vs Year

原来是 2015 年到 2020 年这个时间段得票数最多。该图还推断了人们开始大量使用 IMDb 评分功能的时间段，即 2013 年。下面是对图表的深入分析，它向我们展示了哪一年的投票数最多。

![](img/5b2d5cf743289eeee72d03a41b9d1322.png)

Total Number of Votes vs Year from 2015 to 2020

![](img/4d5fdb6e2e89f71168a39d92d7db6c80.png)

A tabular dataset of the top five years with the most votes.

发现 2016 年录得优秀剧集约 456505 票。据透露，《权力的游戏》制作了两集，促成了这个巨大的数字。《混蛋之战》获得了 181164 张选票，《冬天的风》获得了 125599 张选票。《权力的游戏》第六季一定制作了令人生畏的剧集。

![](img/731821eb806615109a89152a69bc5918.png)

Top five episodes with the most votes.

# 戏剧是评分最高的类型

数据集中有很多类型，比如冒险、动作、犯罪等。大多数电视节目最多有三种类型。

![](img/87f6f798f8649cb580d9e98889ac408b.png)

A horizontal bar chart showing the frequencies of each genre

戏剧是出现频率最高的类型。它在数据集中出现了 143 次。与戏剧相关的电视节目的评级概率为 0.283，高于任何其他类型的概率。

# 收视率最高的一集

进行的另一项分析是为了找出哪一集在《IMDb》中收视率最高。

![](img/ceb51d84b02dce26c315880b0b07be86.png)

Top five episodes based on rating

事实证明，《袭神记》第三季第 17 集 **Hero** 以 10/10 的评分成为无可争议的冠军。作为一个攻击泰坦的粉丝，我是高度知足的。

# 最常见的电视节目

一些电视节目在榜单上出现了多次，而另一些则出现了一两次。电视节目被认为是产生最佳剧集中的最佳剧集的标准之一是在数据集中有多个剧集。因此，数据集被缩短为主要包括出现次数超过三次的电视节目。

![](img/925d7e8b5b83763e5ec7c9aeb5f94fa2.png)

A horizontal bar chart showing the most frequent TV shows

《对泰坦的攻击》以 16 次出现在数据集上的次数再次获得冠军。《权力的游戏》以 14 次出场位居第二。第三个是黑色代码，出现了 9 次。《疑犯追踪》和《绝命毒师》分别排在第四和第五位。

新形成的数据集被进一步分析，以找出电视节目每集的平均投票数和电视节目每集的平均收视率。

![](img/6da57f089442bd98dd0b2903af36641f.png)

A horizontal bar chart showing the most frequent TV shows’ average votes per episode

![](img/c6385169d9f7e23c6eeb75de170e240b.png)

A horizontal bar chart showing the most frequent TV shows’ average rating per episode

在优秀剧集中，《权力的游戏》以每集 65673 票的成绩获得了每集最多的投票。《绝命毒师》平均收视率最高，每集 9.7800。

# 《权力的游戏》vs《绝命毒师》

根据上一节图形可视化中的数字和排名，可以说赢家将在《权力的游戏》和《绝命毒师》之间。

![](img/56482734f5318b05b58ed41f7571736a.png)

Top five episodes based on frequency

根据截断的表格，《对泰坦的攻击》在五大剧集中出现频率最高，但平均有 5154 票。这个数字远远落后于《权力的游戏》和《绝命毒师》，这两部电影的平均票数分别为 65673 票和 53357 票。

此外，在平均评分方面，它也落后于《权力的游戏》和《绝命毒师》，得分约为 9.73。《绝命毒师》和《权力的游戏》分别有 9.78 和 9.74。

《对泰坦的攻击》排在第三是准确的，因为它在数据集中有最多的剧集。这使得《权力的游戏》和《绝命毒师》成为 IMDb 最佳剧集中的两部。

当谈到《权力的游戏》和《绝命毒师》时,《权力的游戏》每集的平均票数比《绝命毒师》多，但《绝命毒师》的平均收视率比《权力的游戏》高。

决定性的因素是他们看到《权力的游戏》以压倒性优势获胜的频率。《权力的游戏》在 IMDb 收视率最高的 200 集中有 14 集，《绝命毒师》有 5 集。

总之，《权力的游戏》拥有 IMDb 最好的剧集。

用于进行这项研究的完整版本代码可以在[**这里**](https://github.com/MUbarak123-56/DataBEL/blob/master/IMDB%20TV%20SERIES%20ANALYSIS.ipynb?source=post_page---------------------------) **看到。**