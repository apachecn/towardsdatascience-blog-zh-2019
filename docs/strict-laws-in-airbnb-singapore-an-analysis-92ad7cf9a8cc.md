# Airbnb 新加坡的严格法律——分析

> 原文：<https://towardsdatascience.com/strict-laws-in-airbnb-singapore-an-analysis-92ad7cf9a8cc?source=collection_archive---------23----------------------->

## 将挑战短期住宿法则的房源比例可视化

![](img/2e89c61791e6e1dd7c6fa0fb4c045767.png)

Photo by [Swapnil Bapat](https://unsplash.com/@deadlyvyper?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 新加坡短期居留法

除了缺乏值得探索的自然景点和是最昂贵的居住地之一外，新加坡无疑是东南亚短期旅行的最佳城市之一，拥有最高效的公共交通系统，实惠的餐饮和干净的环境。

住在 Airbnb 酒店一直是许多旅行者的首选，他们希望在预算有限的情况下探索一些地方，获得一种宾至如归的体验。然而，新加坡颁布了一项针对房东的法律，如果客人在私人房产中停留不到 3 个月，将被处以高达 20 万美元的罚款。更严厉的法律适用于 HDB(住房发展委员会)房产的业主，这是一种设施有限、更实惠的房产。你可以通过下面的链接了解更多。

[](https://singaporelegaladvice.com/law-articles/is-airbnb-illegal-singapore) [## Airbnb 在新加坡违法吗？SingaporeLegalAdvice.com

### 希望通过出租房屋获得额外收入？在房屋共享网站 Airbnb 上挂牌越来越…

singaporelegaladvice.com](https://singaporelegaladvice.com/law-articles/is-airbnb-illegal-singapore) [](https://www.straitstimes.com/singapore/two-hosts-charged-over-illegal-home-sharing-airbnb-laws-in-various-cities) [## 两名新加坡房东因非法合租房屋被罚款:Airbnb 在不同城市的法律

### 新加坡——4 月 3 日，两名 Airbnb 房东因提供未经授权的短期…

www.straitstimes.com](https://www.straitstimes.com/singapore/two-hosts-charged-over-illegal-home-sharing-airbnb-laws-in-various-cities) 

在你犹豫要不要在新加坡预订 Airbnb 之前，先别着急！**客人**在新加坡的 Airbnb 停留任何时间**都不违法**。但由于害怕被罚款，一些客人被公寓保安赶走了。你可以在下面了解更多。

[](https://www.straitstimes.com/singapore/housing/nz-familys-airbnb-woes-highlight-lack-of-clarity-on-listings) [## NZ family 的 Airbnb 困境凸显了房源的不透明性

### 一个新西兰的四口之家出现在加勒比海的吉宝湾，期望拿起公寓的钥匙…

www.straitstimes.com](https://www.straitstimes.com/singapore/housing/nz-familys-airbnb-woes-highlight-lack-of-clarity-on-listings) 

好了，法律已经够了。我们在这里探索新加坡“高风险”房源的分布。在这个项目中，我将在 Airbnb 中使用来自 [**的最新 Airbnb 数据集。**](http://insideairbnb.com/get-the-data.html)

# 数据预处理

在我们深入研究数据集中的要素之前，我想专门针对新加坡禁止短期停留的严格法律创建一个新要素。这将是一个分类特征，取值为“高风险”、“中等风险”或“低风险”。由于私有财产和 HDB 财产分类等可用特征的限制，分类特征定义如下:

*   高风险:最低夜数< 90 天，评论数< 90%
*   中等风险:最低夜数< 90 天，审查数量≥90%
*   低风险:最低夜数≥ 90 天

除了增加一个新功能，我还使用标准的 1.5x +/- IQR 和超过 365 天的最小住宿时间删除了异常价格。此分析不需要的列也被删除。

```
df.head()
```

![](img/c1f0966d0e976073a607c9d799de8081.png)

# 探索性数据分析

## 价格分布

价格的分布与上市的风险几乎没有任何关联。然而，找出上市物业的预期价格范围仍然很有趣，这样我们就可以知道我们在新加坡的平均 Airbnb 住宿的预期价格。

![](img/be4c1fb7a53981002b6e95ac71294d63.png)

上市价格的这种分布似乎是右偏的。如果我们更仔细地观察其按地区的分布，我们随后会发现至少有一个地区不符合总体平均价格。这可以很容易地用一个简单的非参数多重独立样本检验来证实:克鲁斯卡尔-沃利斯检验。

![](img/1fc7771f21139494b9a38b230a68fe95.png)

像任何其他大都市一样，在中心地区看到更高的价格分布并不奇怪，因为大多数游客会在购物区/酒吧/景点/夜生活丰富的中心地区附近闲逛。与任何其他地区相比，中部地区的私有财产比例也要高得多。

## 列表的地理位置分布

很难通过地理位置来可视化风险列表，因为它们往往会相互重叠。下面的填充地图对于查找新加坡风险列表的分布几乎没有任何作用:

![](img/5d89ee145189d34ae0239547eeb6dcf2.png)

A Tableau-generated distribution of listings by risk rating

但一旦按地区划分，很明显，大部分房源都集中在中部地区:

![](img/877f65fcc10a53999ebb05ad5c28ef8a.png)

Credits: [Baval](https://www.kaggle.com/bavalpreet26/singapore-airbnb/)

使用 python 中漂亮的叶库，我们可以大致观察各个地区的房源数量:

![](img/a2d81617891cd17a1d98f641bd6357c1.png)

folium 包允许每个列表的地理位置的交互式可视化。从这里可以很明显地看出大部分房源来自哪里，但是这些房源中有多少是符合法律的呢？

## 符合法律的列表

在本节中，我们将查看符合法律的列表的分布情况:

![](img/f3fc193852a517255b3baabb0821bb9a.png)

我使用评论数量作为感兴趣的特征，因为让许多不同的客人住在最低夜数较低的酒店是有意义的，这最终会导致更多的评论。从这个散点图中，我们可以清楚地看到分布在 90°/180°/365°夜标的图的区别。由于我们无法区分哪些房源是 HDB 的，哪些是私人房产，所以我假设入住至少 90 晚的房源是符合法律的。乍一看，似乎大多数上市公司都不遵守短期居留的规定。此外，某些情节似乎没有意义。以 90 晚最低 285 条评论为例。这怎么可能呢？经过进一步调查，似乎上市在 2017 年法律生效之前就已经存在，这导致了高审查数。此外，该列表只出租可能获得更高评论数的私人房间，因为它将容纳更多的独特客人。

无论如何，让我们通过一个甜甜圈图来看看上市的比例:

![](img/f66a5f6cce574e369651e58a08744db9.png)

当我第一次观察到这一点时，我很惊讶有这么多的主人如此大胆地列出他们违反法律的财产。不过话说回来，由于 Airbnb 在预订得到确认之前不会给出房源的确切地址，这给当局抓住这些房东带来了挑战，尤其是在新加坡的大多数房产都是多层的情况下。在我的分析的最后我会更多地谈到这一点。但是现在，让我们看看风险上市的比例。

## 高风险上市

知道了大部分房源都集中在中部地区，让我们来看看各地区风险房源的分布情况:

![](img/890836cf37b158f4ed1547b3847d5ca9.png)

再说一次，这一点也不奇怪。许多海外客人只是喜欢住在当地景点的附近，而这些景点恰好聚集在中心区域，但是不同类型房间的分布情况如何呢？

![](img/a30b94b717ca9d4f8b3a24ba10a54d2e.png)

现在，我们能够看到符合法律的列表与不符合法律的列表之间的差异。与整个公寓相比，低风险房源的私人房间出租比例更高。我们可以在下面的链接中看到新加坡各个地区的房间/公寓的平均租金。

[](https://blog.moneysmart.sg/property/rent-singapore-cost-guide/) [## 2019 年新加坡租金-租房或租房的成本指南

### 乔安妮·波这么说，你是被这个岛国的高薪承诺和机会吸引，要搬到新加坡去了…

blog.moneysmart.sg](https://blog.moneysmart.sg/property/rent-singapore-cost-guide/) 

新加坡非常高的房租使得租房子而不是整间公寓成为更明智的选择。这恰好是使新加坡成为生活成本最高的国家之一的驱动力之一。Airbnb 产生的额外费用让这种选择变得更加明显。大多数公寓租赁是通过适当的房地产代理或双方之间的私人协议来降低费用。

如果你想知道哪个街区的房源数量最多，我整理了以下 5 个街区的房源数量:

![](img/493d38a20742d93d4189d71f8919e90d.png)

# 拿走

虽然还不清楚是否决定实施严格的短期居留法，但大多数私房业主似乎支持《3 个月住宿法》的决定:

> 2018 年下半年，URA 委托对一千多名私人房主进行的全国调查发现，大多数新加坡人支持拟议的 STA 监管框架。— CNA

[](https://www.channelnewsasia.com/news/singapore/no-change-to-3-month-minimum-stay-duration-for-private-11513474) [## 私人住宅物业的最短逗留时间不变:URA

### 市区重建局(市建局)周三(5 月 8 日)宣布，将维持现行的规例。

www.channelnewsasia.com](https://www.channelnewsasia.com/news/singapore/no-change-to-3-month-minimum-stay-duration-for-private-11513474) 

> URA 维持现状的决定是一个信号，表明它认识到这个问题的复杂性，需要更多时间来研究。— CNA

作为一名私人房产的居民，以及在法律生效前将我的备用房间转租给客人的人，我能够看到硬币的两面(支持和不支持)。

**不支持:**与 HDB 的业主相比，私人业主为现场设施支付额外费用，如游泳池/网球场/健身房/私人停车场等..这些设施有可能被游客滥用，这是非常不雅观的，特别是因为私人财产设施的维护不如公共设施那样详细。

**支持:**随着现代旅行的出现，Airbnb 一直是提供平价住宿的最佳平台之一，每支付一美元就能获得更多空间(例如，以酒店房间的价格购买整个公寓)。作为一个意识到自己消费习惯的千禧一代旅行者，每当我出国旅行时，我都会选择 Airbnb，因为它的价格和便利性。因此，我认为这一举措是针对那些更愿意将旅行预算花在体验上而不是住宿质量上的客人的一种手段。

看着明显不符合短期住宿法的房源比例，我真的很怀疑这项法律的严格性。也许只要客人不会造成任何干扰，就不值得去追捕房主？也许吧。

## 法律漏洞

列出最短住宿时间少于 90 天的房产并不一定意味着房主将房产出租给客人是违法的。

正如我提到的，当客人通过 Airbnb 预订时，将收取费用，作为房主和客人的一种保险和责任形式。房主可能会选择租赁一个月来“评估”他们的客人，然后再延长到 3 个月。

这正是我在加拿大呆了 4 个月进行冬季交流时所经历的程序。房主所要做的就是在他们的 Airbnb 列表中屏蔽剩余的 3 个月，基于信任，我们用现金支付租金。我们设法把整个公寓的租金每月减少了 100-200 美元。

如果你正在阅读这篇文章，请对来自蒙特利尔的卡尔大声喊出来！这是一个非常愉快和难忘的冬天！

## 其他漏洞

房主通知他们的客人让保安知道他们是要来拜访的朋友是很常见的。在新加坡，朋友在别人家过夜并不违法。

这高度依赖于不同公寓的保安。有些人会让你摆脱困境，但有些人会用他们的方式把你赶走，就像可怜的新西兰家庭所发生的那样。

## 你应该注意什么？

如果你仍在阅读，并愿意不顾风险在新加坡预订 Airbnb，请继续阅读。但是请理解，我只是说如果我预订的话，我会怎么做，这并不能保证你不会被驱逐，尽管风险会降低。

*   检查评论和最近评论的数量。如果上一次好评是在你访问网站的几天后，这意味着之前的客人没有被驱逐出酒店。
*   尽量避免在公寓里挂牌，这些地方有保安，他们负责把你赶出去。如果你必须呆在一个房间里，给你的主人发信息，让他/她去警卫室接你。这会让警卫相信你们是熟人。也不要和庞大的群体一起旅行，这只会引起怀疑。
*   无论如何，一定要告诉你的主人，你知道新加坡的短期住宿法律，并为你即将到来的逗留寻求指导。

现在你知道了新加坡的短期住宿法，你会冒险住在 Airbnb 吗？

我知道我会的。

如果你热衷于复制我的作品供自己使用，这里有我的 Github 库的链接:

[](https://github.com/bobbymuls/Singapore-Airbnb) [## bobby muls/新加坡-Airbnb

### 在这个库中只有 3 个感兴趣的文件，这包含新加坡 Airbnb 的数据，这包含…

github.com](https://github.com/bobbymuls/Singapore-Airbnb) 

尽情享受吧！