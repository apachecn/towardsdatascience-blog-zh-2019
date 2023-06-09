# 数据科学和政治风险:关于特朗普、委内瑞拉、古巴、m .卢比奥，有哪些替代数据可以告诉我们

> 原文：<https://towardsdatascience.com/data-science-and-political-risk-what-alternative-data-might-be-telling-us-about-trump-venezuela-f29e6a9e0cbf?source=collection_archive---------23----------------------->

```
For the Spanish version of this article, please click [here](http://bit.ly/2ERPyoV)
```

根据维基百科**，**替代数据是指用于获得对投资过程洞察的数据。对冲基金经理和投资公司内的其他机构投资专业人士经常使用这些数据集。

备选数据集可能包含关于特定公司或事件的信息，但并非特别由所述公司或事件本身产生，然而，由合格的定量分析师或数据科学家进行的数据分析可以提供关于投资机会的独特和及时的见解。

根据维基百科，政治风险是投资者、公司和政府面临的一种风险，即政治决策、事件或条件将显著影响商业行为者的盈利能力或给定经济行为的预期价值。政治风险可以通过合理的远见和投资来理解和管理。

实际上，在我的整个职业生涯中，我一直在为此目的使用替代数据，但从 1998 年开始更加强调这一点。

我希望这篇文章用一个简单(相对而言)但有趣的例子来说明，从 change.org**(委内瑞拉临时总统胡安瓜伊多密切关注的组织)收集的具有政治倾向的数据集如何用于政治风险的原始量化(即波动性是否在增加？递减？稳定？)，它与其他数据结合在一起可用于帮助决策过程。**

![](img/73e24f53d433c3ec4fd50827ae57c4dc.png)

Maduro’s socialist regime is losing support and running out of option. The chat shows number of signed “Pro-Maduro” and “Against Maduro” petitions in change.org since 2012, as compiled by impartial computer algorithms from thousands of online sources

委内瑞拉的情况正在分化美国和世界其他地区的公众舆论，但底线是“反对马杜罗”的激进主义正在战胜“支持马杜罗”的激进主义，这可以通过公正的算法来衡量。此外，特朗普政府显然是这一问题的关键决策者(不是中国，不是俄罗斯，也不是民主党)，我将在下面说明这一点。

Joana Hausmann’s 6 minute tutorial: what’s happening in Venezuela

委内瑞拉的这个问题与我密切相关，因为我是受我出生国当前局势直接影响的许多人之一。我将尝试触及委内瑞拉背景下的替代数据和政治风险问题。

如果你已经知道那里发生了什么，你可以跳过下一部分，直接进入**“结果可视化”**部分。但是如果你需要一些背景信息，请阅读下面的部分。

此外，我发现一个很好的关于委内瑞拉局势的“教程”是 6 分钟 [YouTube 视频](https://youtu.be/bEvHwiJWgAY)，它是由委内瑞拉同胞、纽约人 Joana Hausmann 制作的，讲述了近年来的故事。

![](img/0be50f9a8722a1a569f34f095c8970ac.png)

Illegitimate president Nicolas Maduro, kick starting his “Hands off Venezuela” campaign

## 关于委内瑞拉局势和我的特殊接触的背景资料

80 年代末，在美国繁荣的巅峰时期，我搬到了美国，几年后成为了美国公民。

自 80 年代末以来，委内瑞拉在许多方面逐渐恶化，从鼎盛时期的繁荣到现在的状况:一个充满腐败、贩毒、暴力犯罪、高通胀、饥饿等的国家。与此同时，该国已被证明是世界上石油储量最大的国家。多么讽刺。

![](img/e36e6c5ae9cd597376b3aed150df4a0a.png)

Venezuela is top 3 country in the world with highest rate of intentional homicide as of 2016 according to the World Bank (#1 by 2018 according to my calculations)

1998 年，委内瑞拉军队的一名中校乌戈·查韦斯是当年委内瑞拉总统选举中的害群之马，挑战了两个主要政党，民主行动党和共和人民党。

这两个政党一直在分享权力，就像美国的共和党和民主党一样。

![](img/a767021a727b138733fadbe0eee0a0b4.png)

几年前，乌戈·查韦斯(Hugo Chávez)曾因组织了一场失败的血腥政变而被捕(后来被赦免),那场政变是他和一名名叫迪奥斯达多·卡韦略的军官等人一起组织的，目的是推翻委内瑞拉当时的合法总统卡洛斯·安德烈斯·佩雷斯。查韦斯失败了，他进了一段时间的监狱。

在他通过总统赦免出狱后，他成立了一个政党，PSUV 或“委内瑞拉联合社会党”，多年来，尼古拉斯·马杜罗、迪奥斯达多·卡韦略、拉斐尔·拉米雷斯(PDVSA 国家石油公司前总裁)和其他人都加入了该党，成为高级成员。

查韦斯不知从哪里得到了普通民众对他的社会主义理想的支持。一个挑战体制的“政治摇滚明星”，在委内瑞拉之外几乎无人知晓。

那时(1998 年)，我在美国国际集团华尔街 72 号的风险金融部门工作。我是少数几个被聘用的定量分析师之一，利用金融分析和数据科学来研究替代数据，用于新产品开发，并帮助投资和保险承保经理的决策过程。AIG 真的在雇佣“火箭科学家”，他们是直接来自 NASA 的博士，他们中的一些人最终和我一起工作，还有你那些来自对冲基金和投资银行的“更传统的定量分析师”;工商管理硕士，工程和计算机科学背景。

AIG 持有大量委内瑞拉和 PDVSA 债务，委内瑞拉债券的价值以及 AIG 投资组合中的项目融资敞口存在很多不确定性。如果这个乌戈·查韦斯做了一些激进的事情，比如拖欠国家的所有债务，会怎么样？我们如何评估委内瑞拉的政治风险并据此调整我们的立场？

![](img/10aaa49c6580c890e4f89015f773466b.png)

General Raul Salazar, Hugo Chávez first Minister of Defense, later removed due to difference of opinions with Chávez and Diosdado Cabello due to difference of opinions around relationships with the U.S. government

AIG 的一位高层人士知道我是委内瑞拉人，他漫不经心地问我，关于委内瑞拉的未偿债务，我对乌戈·查韦斯有什么看法。我说:“我没什么看法”。但后来我回答说:“我们为什么不直接问雨果·查韦斯呢？。这几乎是一项不可能完成的任务，因为在委内瑞拉以外没有人知道他是谁，也不知道如何接近他。

我获准在选举前接近雨果·查韦斯。通过家庭关系，我联系了委内瑞拉驻华盛顿的武官 Raul Salazar 将军，我认为他可能是最好的办法，因为我知道 Salazar 将军在委内瑞拉军事学院与查韦斯有过交往(我的预感是对的，Raul Salazar 将军后来成为查韦斯的第一任国防部长)。

萨拉扎将军是我和我妻子的朋友，几年前我们在华盛顿认识的。我做过一项非常有趣的咨询任务，涉及对委内瑞拉武装部队养老基金的蒙特卡洛模拟分析。我必须向委内瑞拉武装部队各军种的参谋长们展示结果，我还与萨拉扎将军建立了友谊。

无论如何，在要求与 Hugo Chávez 会面的两天内，Salazar 将军在加拉加斯安排了与 Chávez 及其团队的会面。这次会议在许多方面都很有趣。出席会议的有 AIG 的三位高管(包括我)、Hugo Chávez 和他的两位最亲密的合作者。

直到我遇见雨果·查韦斯的那天，我对他的看法一直很负面。亲自见到他并了解他的理想使我改变了对“司令官”的看法。我仍然认为他的直属团队是不合格的，但也觉得查韦斯的意图是好的；精力充沛、颇具魅力的理想主义者。

我承认:1998 年，我在委内瑞拉总统选举中投了当时的候选人乌戈·查韦斯的票。对大多数委内瑞拉人来说，他的社会主义思想看起来不错，他光明正大地赢得了第一次选举。

但我不知道(也不知道其他任何人)查韦斯及其亲信的意识形态已经被古巴共产党和卡斯特罗兄弟所塑造。

![](img/87e48a33eaadf37e6178c2b7369b521b.png)

On the left is Raul Castro, center Rafael Ramirez, President of PDVSA from 2004–2014 and now Nicolas Maduro and the USA nemesis, and Diosdado Cabello, right.

时间快进许多年，我了解到查韦斯核心集团的人多次有意试图阻止公共管理的透明度。移动，例如:

*   通过法令，而不是公开招标，将石油权授予与他的意识形态相近的人。
*   有效解散 PDVSA 金融公司(国家石油公司的融资工具，允许他们获得廉价融资)以避免合规和监管监督。
*   将采矿权授予资金不足的“纸”公司，这些公司由与查韦斯意识形态结盟的人经营。
*   由前上尉、乌戈·查韦斯的前保镖亚历杭德罗·安德拉德经营的主权国家财富基金(FONDEN)人为操纵货币兑换以有利于某些实体。

![](img/329d3ea2f61051b011d7e055c8fc12f3.png)

The Chávez/Maduro’s regime is crumbling under its own weight

除了上述许多问题之外，多年来，有证据表明，对普通公民、记者和反对派政治家的镇压试图将查韦斯以及后来的马杜罗“社会主义政权”的负面影响公之于众。

现在，大多数委内瑞拉人后悔投票给他和他的失败的社会主义实验，这几乎使这个国家破产。该国希望变革，希望与传统盟友(查韦斯之前)建立更紧密的关系。

该政权与军队和警察的腐败、对政治对手的酷刑、操纵选举、援助恐怖组织、封锁新闻自由等联系在一起。

多年来，我一直想知道美国媒体在这些问题上有什么样的“沉默的阴谋”，因为猖獗的犯罪、酷刑、恐怖主义等新闻没有得到遏制。，从未登上美国主流媒体。

委内瑞拉的朋友和亲戚通过 YouTube、脸书等分享的视频。描绘了街头的法外处决，人们吃垃圾，人们在街头抗议中被活活烧死，委内瑞拉国民警卫队用中国制造的军车碾过并杀害人们，准军事组织用俄罗斯制造的武器杀害抗议者，等等。从未被主流媒体报道过。

但在最近 6 个月左右的时间里，几乎不可能在新闻中看不到任何与委内瑞拉有关的内容。每个人都有自己的看法。有什么变化？

Alexandria Ocasio-Cortez position about Venezuela

当然，美国政府显然不希望中国和俄罗斯出现在美国的后院，并且可以获得世界上最大的石油储备。这个问题很复杂，而且只是因为我个人不同意特朗普政府的一些问题；我不会反对他做的每一件事。

如果你问，90%的委内瑞拉人会说他们更喜欢美国作为商业伙伴，而不是中国或俄罗斯，或者更糟的是古巴。但如果你问与这个问题没有利害关系的人，他们大多会反对特朗普或没有意见，并声称正在发生的事情是美国的干涉主义、帝国主义，无论你想怎么称呼它。

![](img/9c4cd0801ba2862d613809a716b7fc43.png)

Mexican American Journalist Jorge Ramos of Univision recently became part of the news, when he was detained by Maduro’s security staff and equipment confiscated. His crime was showing Maduro’s a video of Venezuelan people eating our of a garbage truck; which enraged Maduro and his staff. Jorge Ramos is a well known anti-Trump activist, but even Jorge Ramos is supporting what the Trump administration is doing in Venezuela.

就像 Joanna Hausmann 在她的视频中说的那样，“对话已经偏离了真正重要的东西，委内瑞拉人民”，这篇帖子的数据科学方面处理的是 ***内容理解*** ，即量化人民谈论主题的集体声音；和对参与问题的各方的理解，以及他们的利害关系。

下面的方框中简要强调了如何将此用作投资决策 的 ***部分，因为该主题非常广泛，而且方法大多是专有的。***

相比之下，这是我自 1998 年以来为许多大公司部署的更复杂模型的粗略版本，但原理是相同的。其中一些一般性的想法首先在我的创业公司“ttwick”中使用，在那里我能够为我的 R&D 中的一些新颖的机器学习算法申请专利(我的专利最终被对冲基金 Elliott Management Associates 收购，这是世界上最大的激进对冲基金，由亿万富翁慈善家保罗·辛格(Paul Singer)所有。)

```
Personally, I want things to change in Venezuela: free and transparent elections, just like the U.S. government is advocating. Recently, there have been large purchases of defaulted Venezuelan debt by a Connecticut based hedge fund (the country is behind on USD $10 billion of payments on bonds issued by the Chávez/Maduro regime).At this precise moment (March 4th, 2019), buying defaulted bonds looks like a very interesting and aggressive contrarian position, when most holders of Venezuelan debt are willing to offload their bonds for practically nothing. Is this a good indicator that change is about to happen? Are things in Venezuela reaching a break-point?This is the sort of things you can analyze for hedge funds and that present a great deal of opportunities for machine learning and artificial intelligence tools. If you look around, most finance related machine learning projects out there are just "financial technical analysis systems" rebranded as "artificial intelligence" by people with no domain expertise in finance. But the incorporation of automated news analysis, court fillings, people's opinions around key political issues, activism, etc. all have value when properly analyzed. And in my opinion, there is a much better "return" when used to analyze debt than equity.Anyway, since I still know a lot about what's going on in Venezuela from several traditional and non traditional sources, it looks to me that this Connecticut hedge fund might be making the right move.
```

在这篇文章中，我不会分析成千上万的来源，比如我过去运行的项目，等等。，但出于简单起见和时间限制，只有一个来源。从构思，到写代码，到画面可视化，到图表，到写这个故事，我不想花超过 4 个小时的时间。

我使用的来源是 change.org。

# Change.org

根据他们的网站，Change.org 是世界上发展最快的社会变革平台，授权超过 2 亿人在他们的社区创造变革。

Change.org 的人们与决策者一起为影响他们生活的大大小小的问题寻找新的解决方案。据他们说，他们已经在 196 个国家赢得了 33，409 场胜利。

我选择这个网站，因为它或多或少以一种透明的方式捕捉到了像你我这样的人对一项事业的意图。

![](img/6a3527188d8b7216a92ebbdb79ee7066.png)

Change.org search. 297 results containing the word Venezuela. Examples of unstructured data in this page

然而，由于请愿书在这个网站上是非常自由的形式，所以需要做大量的自然语言处理来消除术语的歧义和组织数据。例如 UN = ONU(西班牙语中的 UN)。

此外，由于请愿书可以用任何语言书写，我们还有一个额外的挑战。该项目如下:

1.  数据收集和清理
2.  翻译和歧义消除
3.  标记
4.  形象化

当我在周末思考这个问题时，我了解到 Change.org 曾经有一个 API，但被弃用了。因此，除了编写一个 Python scrapper 和使用 BeautifulSoup，我没有别的方法来获取数据。

截止到 2019 年 3 月 2 日的经过清理和消歧的数据集就在这个 [GitHub](https://github.com/lmsanch) 库中，还有我写的 scraper，不言自明。

## Python 美丽组码

下面，你可以找到 Python 代码。您可以运行它并传递 Python 字典以导入到 pandas 数据框中。

如果您知道一些基本 NLTK 和 SciKit 知识，您可以自己做分类器和消歧，我在这里不做介绍。

[](https://github.com/lmsanch/change-search/blob/master/petition.py) [## LMS anch/更改-搜索

### 一个美丽的网站 change.org 汤刮刀。为 lmsanch/change-search 开发做出贡献，创建一个…

github.com](https://github.com/lmsanch/change-search/blob/master/petition.py) 

# **结果可视化**

change.org 的相关请愿被分为“反对马杜罗”和“支持马杜罗”两类。由于语料库很小，手动标注是首选。例如，向"国际法院"提交的请愿书说"调查委内瑞拉 X 大屠杀"，被归类为"反对马杜罗"，因为它涉及对委内瑞拉司法系统缺乏信任等问题。

## 数量和时间序列

结果涵盖了从 2012 年 Q2 奥运会到现在的请愿活动。

![](img/73e24f53d433c3ec4fd50827ae57c4dc.png)

Distribution of “Pro-Maduro” vs “Against Maduro”

如果我们看看分类请愿书的时间序列，就会发现另一种见解，即 2019 年出现了一股强大的“亲马杜罗”力量，这是自 2015 年 Q1 以来我们从未见过的。

![](img/50619a02d9e05bdcdf88edff7de3fbda.png)

Distribution of “Pro-Maduro” vs “Against Maduro” petitions over time

如果我们观察请愿和发起人(人和地点)的相对规模，我们会得到有趣的见解:

![](img/d1464405398328576e05f6ae4d1f8deb.png)

The petition with the most supporters in a petition “Against Maduro”, addressed to the International Court of Justice

如果我们“放大”到“支持马杜罗”的请愿书，我们会看到高度集中在一个人身上:

![](img/7688a25a3e854e6007689567aa7a7bc0.png)

The largest petition does not have a valid originator, and the other ones are mostly originated by “Robert Naiman”, who does not sound like a Venezuelan name.

## 请愿书的来源

让我们来看一个包含“支持马杜罗”和“反对马杜罗”数据的汇总表。

![](img/5b660c245aaa713bfbe4dc6634f8f1ec.png)

Pro-Maduro Table

在 10 份“支持马杜罗”的请愿书中，我们看到最大的一份来自委内瑞拉，但发起人是匿名的。

![](img/71398aeebfae088b76304b7c958b93a5.png)

I ask: What is somebody who specializes in Middle East issues doing in Venezuela? A data outlier

此外，我们看到，在剩余的 9 个签名中，有 3 个来自华盛顿特区，由一个叫“罗伯特·奈曼”的人发起，几乎占了我们在 2019 年看到的所有推送，此外还有“放开委内瑞拉”，只有 416 个签名，由美国的一个叫“亚历克斯·坎贝尔”的人发起。(关于马杜罗发起“放开委内瑞拉”运动的视频，请点击[此处](https://www.youtube.com/watch?v=UpHmBHcYI7Q)。)

在我看来，这些请愿书不是关于委内瑞拉问题的有机和真诚的请愿书，而是反特朗普的政治问题。

```
Upon further investigator, [Robert Naiman](https://www.justforeignpolicy.org/about/staff/) appears to be some sort of lobbyist based in Washington D.C. According to Wikipedia, "Robert Naiman is Policy Director at Just Foreign Policy and on the board of directors at progressive news organization Truthout. He has master's degrees in Economics and Mathematics from the University of Illinois. He writes on U.S. foreign policy at Huffington Post and is a frequent commentator on the region's events". 
```

相比之下，“反对马杜罗”的请愿书看起来非常有机，主要由委内瑞拉和世界各地的委内瑞拉人发起。该表包含的条目比显示的多得多。

![](img/4caee7681f6374f1f3b87273ca50c98e.png)

“Against Maduro” Table

![](img/5df540ee6197f11c038fca8c54a4f557.png)

“Against Maduro” petitions are mostly originated in Spain, Venezuela, the United States, Ecuador, Canada, and Trinidad and Tobago; while the “Pro-Maduro” petitions are mostly originated in Venezuela (anonymously) or in the United States via Robert Naiman

## 请愿的语气

鉴于我给自己设定的时间限制，这是一个有趣的探索方面。所以，我认为最简单的方法来产生一些知识，抓住请愿书的意义，是产生一个词，可以通过签名的数量来加权。虽然我可以使用定制的 python 代码来生成单词 cloud，但是我使用了[这个](https://www.wordclouds.com/)服务。这些是步骤。

*   请愿的串联字符串标题乘以其相对频率的整数+ 1
*   消除停用词
*   删除“委内瑞拉”一词
*   词频高的封顶(试错)，直到词云看起来没问题。

这就是结果。 ***犯罪、法庭、法律、*** 司法等。是“反对马杜罗”图表中最相关的术语。几乎所有的单词看起来都与我相关，但我注意到“大象”和“Ruperta”这两个词没有意义。但是进一步检查内容，现在它是有意义的(阅读下面的“其他”一节)。

![](img/21398d2002796145850bf6da52e5d24e.png)

Against Maduro Word Could: A cry for help evolving over time. Words such as Crimes, Help, ICJ, Justice, Court, UN, Legal, Starving stand out.

![](img/0e89a9beece6bfbf718bf154a02b38ec.png)

“Pro-Maduro” word cloud: avery authoritative “tone” concentrated in 2015 and 2019\. Words such as Immediately, Must, Stop, Surrender, Executive, Congress, War, etc stand out.

## 请愿书是寄给谁的？

看起来美国在“支持马杜罗”和“反对马杜罗”方面有很大的分量，在下面的名字上有经典的[帕累托分布](https://en.wikipedia.org/wiki/Pareto_distribution)。

![](img/f25af2adff288c3772e3105f55f45964.png)

Screenshot of Pandas groupby. Left, “Pro-Maduro” petitions. Right, “Against Maduro” petitions

![](img/99b894fc49b7cfc6afbf36ff7ee61f0e.png)

According to my metrics, the “Against Maduro” weighted petitions were addressed to this group: ICJ, OAS, Secretary-General of Organization of American States, Luis Almagro, President of the United States, Senator Marco Rubio

![](img/02336fc13405060cef7e19534435af36.png)

According to my metrics, the “Pro-Maduro” weighted petitions were addressed to this group: President of the United States, U.S. House of Representatives, U.S. Senate, U.S. Secretary of State, Australian Parliament

## 一幅画胜过千言万语

用于在社交媒体、博客、短信等中宣传请愿书的图片。传达大量信息，这些信息可以用来增强我从基于文本的信息中提取的知识。

虽然使用计算机视觉从这个语料库中提取知识超出了本文的范围，但下面是前 5 名“支持马杜罗”和“反对马杜罗”请愿书中使用的图像链接(这可以让你知道为什么“国际法院”是委内瑞拉人解决他们问题的最高实体)。

```
warning: Some of the images can be very graphic.
```

“反对马杜罗”请愿书(大部分是用西班牙语写的):

*   [国际刑事法院:调查委内瑞拉政府的反人类罪](http://assets.change.org/photos/9/rs/xx/RkrSxxvbVimhXHr-800x450-noPad.jpg?152097908)
*   [世界公民保卫委内瑞拉联合国/国际法院/美洲组织](https://assets.change.org/photos/5/kn/cj/mjkNCjmydSRYrqB-800x450-noPad.jpg?149388054)
*   [委内瑞拉----反对在奥斯卡·佩雷斯大屠杀中侵犯人权和违反条约的正义(T11)](https://assets.change.org/photos/1/tn/lg/ZGTnlGwVOTfhLHJ-800x450-noPad.jpg?151667490)
*   [Investiguen Gobierno de Maduro por Crímenes de Lesa Humanidad(调查马杜罗政府的反人类罪)](https://assets.change.org/photos/3/rb/cc/DURBccGySnDPxBV-800x450-noPad.jpg?152192153)
*   [请求委内瑞拉立即进行军事干预或人道主义干预](http://assets.change.org/photos/2/mh/bz/iCMhbzBGEycIvMD-800x450-noPad.jpg?154585864)

“支持马杜罗”的请愿书(大部分用英语撰写):

*   [立即撤销针对委内瑞拉的行政命令](http://assets.change.org/photos/0/xc/to/gCXctOcQdgKWwNY-800x450-noPad.jpg?152306929)
*   [@SenatorDurbin:抵制川普违宪的委内瑞拉政权更迭战争](http://assets.change.org/photos/8/vy/gc/ptvygcqMJOmaHyd-800x450-noPad.jpg?154862192)
*   [国会:明确禁止未经国会授权的战争](http://assets.change.org/photos/4/iy/zm/AciyZmfzRzOTvaQ-800x450-noPad.jpg?155113438)
*   [告诉@CoryBooker &国会阻止特朗普对委内瑞拉的政权更迭战争](http://assets.change.org/photos/3/sv/ev/jaSvEVdTnRMJRBF-800x450-noPad.jpg?154923346)
*   [美国远离委内瑞拉](http://assets.change.org/photos/0/sz/cd/dFszcdgOEnrFyWC-800x450-noPad.jpg?154905807)

## 其他的

正如我前面提到的，单词“Ruperta”和“Elephant”在单词云中显示为语义异常值。2017 年 4 月 3 日，一份关于帮助加拉加斯 Caricuao 动物园饥饿大象 Ruperta 的请愿书启动，引起了很大的反响。

委内瑞拉的所有动物园都是由社会主义国家管理的，它们都达到了可悲的条件(当人们吃执政政府领导人的垃圾和剩菜时，你能指望什么？)来自佛罗里达州克利尔沃特的韦伯·道利斯先生，显然是一个关心动物和动物权利的人，想要为此做点什么(你可以在这里阅读他的请愿书)。

不幸的是，[鲁珀塔去世](https://www.express.co.uk/news/nature/975860/venezuela-elephant-ruperta-symbol-caracas-zoo)。在社会主义的委内瑞拉，大象 Ruperta 并不是唯一挨饿的动物。许多已经被饥饿的人群吃掉了。

以下是一些动物爱好者在委内瑞拉发出的急切呼吁。你无法想象这让我有多难过。这简直是犯罪。

![](img/aea6b33cd47222f48b9f6ac303d2e742.png)![](img/e850e7142f7608ba431c55ca78c3e8b2.png)

Even animals have been affected by the incompetent regime in Venezuela. The stories are extremely sad.

## 我的结论

现在，我个人觉得，当美国主流传统媒体选择报道一个比另一个更受重视的话题时，他们“有一些东西”。

![](img/23d22f92c9fa8e952930028b586225a2.png)

It feels to me that US news outlets have made a bigger deal of the US President meeting the dictator on the right, compared to the US President meeting the dictator on the left. And to leave aside doubts about my political leaning, I voted for Barack Obama in 2008 and again in 2012.

关于委内瑞拉问题，嗯，我有偏见:我认为委内瑞拉是一个失败的社会主义实验。我认为联合国人权事务高级专员、智利前总统、智利社会党领袖米歇尔·巴切莱特并不关心委内瑞拉正在发生的事情。即使在许多人和机构的多次请求下，她仍拒绝访问委内瑞拉，也拒绝给马杜罗政权贴上标签。她不在乎仅仅是因为委内瑞拉失败的社会主义实验给了社会主义一个坏名声。

![](img/5229bbeef931cb0b7805fd89f5aef33f.png)

Chile’s President Sebastian Pinera sharply criticized his leftist predecessor and UN rights commissioner Michelle Bachelet Sunday for failing to condemn Venezuela’s socialist President Nicolas Maduro for human rights violations.

我个人认为，约翰博尔顿和迈克·蓬佩奥设置的策略非常聪明，而以胡安瓜伊多为临时总统的委内瑞拉自由透明选举的关键是对古巴施加压力。关键可能是美国国务院最近对古巴政权采取的伤害他们的行动:资本自由流向古巴。在这篇文章中，我想从数据科学、编程和政治的角度讲述很多东西，但我需要保持内容简短。事实上，它已经很长了，涵盖了 2-3 个不同的领域。

我希望这个“数据科学”实验及其背景信息能让你对这个主题形成自己的看法。我很好奇你是怎么想的。美国在做正确的事情吗？

无论你有什么样的问题，我都希望收到你的来信。我还想创建一个回购，并使其成为我的第一个开源(我所有的回购都是私人的)项目，围绕像这样的政治问题的内容理解，重用我的私人回购的选定部分。

如果你喜欢这篇文章，一定要给它一些掌声。你可能想看看我其他关于数据科学和金融、健身、音乐等的不拘一格的帖子。你可以关注我的私人回复[这里、](https://sourcerer.io/lmsanch) twitter 帖子[这里](https://twitter.com/lmsanch)中的活动，或者你可以问下面的 Qs 或者在 SGX 分析的[给我发邮件](mailto:luis.m.sanchez@sgxanalytics.ai)。

干杯