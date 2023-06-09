# EPL 幻想 GW13 回顾和 GW14 算法精选

> 原文：<https://towardsdatascience.com/epl-fantasy-gw13-recap-and-gw14-algorithm-picks-f5161c390ece?source=collection_archive---------30----------------------->

我们的钱球方法的幻想 EPL(队 _id: 2057677)

![](img/49b5e91c465dd9868983433d3db138e4.png)

如果这是你第一次登陆我的幻想 EPL 博客，你可能想先看看[第一部分](/beating-the-fantasy-premier-league-game-with-python-and-data-science-cf62961281be)、[第二部分](/epl-fantasy-is-one-week-away-and-our-algorithm-is-ready-to-play-78afda309e28)、[第三部分](/epl-fantasy-gameweek-1-stats-and-algorithm-recommendations-for-smart-picks-23b4c49cae8)、[第五部分](/epl-fantasy-gw3-recap-and-gw4-algorithm-picks-bc384ce1374b)和[第九部分](/epl-fantasy-gw8-recap-and-gw9-algorithm-picks-b618c5291762)，以熟悉我们的整体方法和我们随着时间的推移所做的改进。我在这个项目中的犯罪搭档是 Andrew Sproul，他和我一样对数据科学、人工智能和幻想 EPL 充满热情。

本周我们将保持简短，因为我们已经在前面的博客中描述了我们的方法和主要更新。

# GW13 世界排名前 100 的选手

![](img/446ede0139c63d913a36f9263506828f.png)

与平均得分 49 相比，世界排名前 100 位的球员又度过了强劲的一周！尽管如此，还是有一些前 100 名选手的分数在 50-60 之间，所以如果你的分数接近或超过这个范围，你仍然可以对自己感觉很好。

现在我们有三个玩家突破 900 大关，相当可观！

# EPL 100 强球员最佳混合团队

当我们谈论世界前 100 名球员的话题时，让我们看看谁在他们的球队中最受欢迎，以及 GW11 最受欢迎的球队阵容。

## 前 100 名最佳守门员

![](img/581125feb1a9deafd318ac431cd1eb5f.png)

## 前 100 名中最受欢迎的捍卫者

![](img/e62bf1176d4b018c74eb69020c381f68.png)

## 前 100 名最佳中场球员

![](img/d80a807e79f38e9001826d5952533176.png)

## 前 100 名中入选最多的前锋

![](img/19f3adca9d134b7ee040e6d30e54f4c4.png)

看起来现在有更多的人选择了拉什福德，也有一些顶级球员对奥巴姆扬很固执，仍然让他留在他们的球队，希望获得一些投资回报。

我们使用这些数据和当前的球员价格来创建下面的球队，这是由前 100 名中最受欢迎的球员组成的:

![](img/b41e2d4c6eeafa9644c2e0f47b6255f9.png)

看起来不错的团队，在关键位置上有很多尝试不同选择的余地，同时仍然保持一个坚实的球员核心。

## 前 100 名 Fantasy 用户选择最多的团队

然而**3–4–3 仍然是首选阵型**，旨在优化他们的进攻球员获得的总积分，这些球员通常有更高的机会获得助攻、进球和总积分。

![](img/728a0636dab3c47ee82a528c6826530a.png)

# GW13 团队绩效总结和总体统计

对我们来说，体面的一周，59 分，高于平均水平 49 分。我们的队长人选还不错，但我们对 Auba 的期望更高。

![](img/4c5289b0324f5c92ee7b6aad06a3a3bf.png)

# GW13 整体统计数据为我们的 GW14 选秀权提供信息

下面让我们从调整后的未来三个比赛周的对手难度等级(FDR)开始:

![](img/cadf8afa4e2aa1d47708b3ddd3b6f8ac.png)

阿斯顿维拉、布莱顿、埃弗顿、伯恩茅斯和伯恩利是仅有的 FDR 得分超过 75%的球队**。**我们的算法是这样写的，它不会在本周推荐从这些球队购买球员。赛程相对轻松的球队有**阿森纳、南安普顿、莱斯特、谢菲尔德联队和切尔西，**所以从招募新球员，这些球队可以在接下来的三场 2-3 场比赛中获得回报。

# 美国东部时间 11 月 27 日晚 9 点最新伤情更新

以下数据来自一个独立网站，该网站更新最新受伤情况的频率比 Fantasy 网站高得多:

![](img/12571d899eae764a717c4f47d74ba996.png)

接下来，让我们通过 ROI 和 pts_per_90min 统计数据来看看顶级球员:

**投资回报率排名前十的守门员**

![](img/60bccfe6529c5a5c721160d9dfa5489b.png)

**90 分钟内排名前 10 的守门员**

![](img/e2de08c794b070f37980bae396ebe030.png)

**按投资回报率排名的前 10 名防守队员**

![](img/e812ddd2c66402fad0fd30eb68b36883.png)

**按 pts _ per _ 90 分钟排名前 10 的防守队员**

![](img/58029ff02614554ed7476a66109b20fe.png)

**投资回报率排名前十的中场球员**

![](img/d89fb1e81a878371728370f7115c8638.png)

**90 分钟 pts _ per _ 强中场**

![](img/79fa1559c92a95479f1b5a43da10dcda.png)

**投资回报率排名前十的前锋**

![](img/fd7d84c6fda86a7475a51b9a289c686b.png)

**射手前 10 名由 pts_per_90min**

![](img/5e1c14696adf1240cffaa521d220cda1.png)

# GW14 算法选择

提醒一下，我们的算法会考虑**调整后的每队阵型预算**，并尝试**最大化主要 11 名球员的每个位置的支出**，然后让你的替补获得良好的 ROI 值。根据当前的投资回报率得分，在接下来的三场比赛中过滤掉任何具有 AVG 对手难度(FDR≥75%)的球队，并从可用选择列表中删除受伤的球员，我们的算法选择了以下球队作为当前花费全部 1 亿美元预算的最佳球队:

![](img/9646b4b86fe53843bcf29237269453c7.png)

在我们看来，这是一支相当平衡的球队，银行里有整整 120 万英镑，可以用来试验和尝试不同的球员配置。

就我们自己的球队而言，我们决定不做任何突然的举动，只是摆脱了我们的第二个 GK——里卡多——并以 400 万英镑的价格得到了一名非上场门将，以便为下周的更多转会腾出资金。在上周淘汰万-比萨卡之前，我们给了他最后一次机会来拿分。

![](img/8bf321783e52ec7d7de34039dc7a1f49.png)

# 团队统计

看看**最佳/最差防守和进攻**可以有几种不同的用法——例如，如果一个最佳进攻队与一个最差防守队比赛，你可能想让你的进攻中场或前锋担任队长。此外，当你查看这些位置的算法建议时，你可能想优先考虑防守最好的球队的 DF 和 GK。

# 最佳 7 项防御

![](img/abade63d0b36a1d24b239bf73ba1f580.png)

# 最差的 7 种防御

![](img/0f3417fd3716486a41b574287d359740.png)

# 最佳 7 项犯罪

![](img/f334ca07fc4459048d74f934a468efcd.png)

# 最糟糕的 7 项罪行

![](img/9e569078c69e450960da8fc01e922e17.png)

# 累积团队投资回报统计

下面你可以看到球队，按累积玩家投资回报率排序。请注意，**活跃玩家是任何已经玩了总可能游戏时间的至少 33.33%** 的玩家。例如，总可能分钟数=周数* 90 分钟= 13* 90 = 1170。所以，我们把所有至少打了 1080/3.3 = **351 分钟**的球员都算作该队现役球员。

![](img/c74e8adc45d06c3cb5c3848e14ce5f15.png)

在我们将比赛的最短时间增加到 1/3 后，莱切斯特遥遥领先。看起来他们或多或少使用相同的 11 名球员，他们一直表现得相当稳定，给了他们比其他人高得多的 avg_palyer_roi 和 avg _ team _ ROI。随着越来越多的球员进入 Pep 轮换，曼城的 avg_team_roi 统计数据甚至下降了，最近的表现也不那么令人信服。

# 最终想法:

大家感恩节快乐，别忘了疯狂的 12 月 EPL 马拉松赛将于下周 12 月 3 日(周二)开始，所以别忘了在周二早上准备好你的替补！！！