# 使用分类预测启动失败

> 原文：<https://towardsdatascience.com/predicting-startup-failures-using-classification-8e11d2703e0a?source=collection_archive---------28----------------------->

![](img/723c486a8d97c9cfabd9a943869305fb.png)

[Unsplash](https://unsplash.com/s/photos/Startup?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

这个项目是名为 Metis 的沉浸式数据科学项目的一部分。你可以在我的 [*GitHub*](https://github.com/alisonglazer/metis_project_3) *和幻灯片* [*这里*](https://www.slideshare.net/AlisonGlazer/metis-project-3-predicting-startup-success) *找到这个项目的文件。最终的模型在这里是可访问的*[](https://startup-predictor.herokuapp.com/)

## **一点背景知识**

**最近，我测试了一系列分类算法，看看我能否使用 [CrunchBase 数据集](https://data.crunchbase.com/docs/daily-csv-export)预测一家初创公司是否会失败。通常，有人需要一个企业帐户来访问这些数据，但我能够在不久前找到一个副本。CrunchBase 是风险投资公司了解他们可能投资的公司的绝佳资源。他们中的许多人为企业访问支付额外费用，以获得高级搜索等附加功能。**

**对于这些公司来说，使用这些数据和机器学习工具来预测潜在投资在未来可能会如何发展将是有利的。这是因为风险投资会接触大量不同的公司，但只投资其中的一小部分，审查所有公司真的很乏味。拥有相关的领域知识会有所帮助，但是，有了 CrunchBase 上的所有可用数据，应该可以在没有太多先验知识的情况下做出一些决策。**

**此外，随着初创公司保持更长时间的私有，后期投资最近变得越来越受欢迎。这产生了更多关于早期业绩的数据，我用这些数据构建了一个工具(将在 CrunchBase Enterprise 等平台上使用)，以帮助比较公司并预测它们的成功机会。**

## **该过程**

**CrunchBase 数据集提供了一个全面的公司列表，其中包含大量关于它们的信息，以及它们每一轮融资和单个投资的明细。由于创业环境不断变化，我只研究了过去 10 年内成立的公司。我也排除了那些只进行了一轮融资就失败的公司。成千上万的公司被分为两组:失败的公司和成功的公司(仍处于早期阶段的公司也被排除在外)。这给我留下了大约 10000 家公司。**

**清理完所有数据后，我就可以设置所有感兴趣的特性了。这些信息包括每家公司的融资轮次、行业和地点。一旦我做好了所有这些准备，我测试了相当多的分类模型，以找到最好的一个。下面是每个基线模型的 ROC 曲线图。**

**![](img/5e3027cd9b3ba5c55e99845cc7a5f7ad.png)**

**ROC Curves for each baseline classification model**

**我用它和另一个指标来比较每个模型:f_beta，它是召回率和精确度之间的加权调和平均值。我将 beta 值设置为 3，这意味着召回比精确更重要。当考虑风险资本投资时，大部分回报通常来自不到 20%的投资。更重要的是抓住所有潜在的独角兽，即使是以投资相当多的废物为代价。考虑到一只独角兽可以轻松获得超过原始投资 100 倍的回报，取消其中一项需要相当多的“哑弹”。**

## **结果**

**在建立了最初的模型后，我挑选了最有希望的模型，并调整了它们的各种超参数，以找到预测能力最强的模型。(为了简单起见，这个我就不赘述了。如果对这个过程有任何疑问，请随时联系我们。)考虑到用例，可解释性对我来说也是一个优先考虑的问题，所以我更关注逻辑回归和基于树的模型，它们具有很高的可解释性。**

**选择的模型是逻辑回归，它将公司的成功几率作为前面描述的特征的函数来计算。这款车型的 f_beta 评分是 0.85 分满分 1 分，相当不错。**

**作为一个基线，任何拥有超过一轮融资的公司都有 31%的成功机会，其自身的一系列功能可以提高或降低这个数字。下面是这些特征系数的细目分类。如果条形向左延伸，会增加失败的几率，向右延伸会增加成功的几率。**

**![](img/25b99b32b134aaddef34dcd6ad986227.png)**

**Logistic Regression Coefficients in terms of Log Odds**

**不足为奇的是，一家公司筹集的资金越多，就越有可能成功。我发现，一家公司每轮融资额外增加 100 万美元(平均而言)，他们成功的几率就会增加 16%。我对两轮融资之间的时间间隔感到惊讶。一般来说，一家公司在两轮融资之间的时间越长，对他们越有利；融资周期之间每增加一个月，成功几率就会增加 5%。种子期和首轮融资之间的情况不同，每增加一个月，这些几率实际上会降低 3%。**

**我发现的另一个特别有趣的特征是在行业内部。所有最受欢迎的硬件行业(包括制造业、清洁技术和生物技术)中的公司更有可能失败。这很可能是因为在寻找可随公司发展而扩展的可靠供应商时，成本和复杂性增加了。**

**如果你想亲自尝试一下，请访问我通过 Heroku [这里](https://startup-predictor.herokuapp.com/)部署的应用程序。有任何问题，请随时联系[和](mailto:alisonglazer@gmail.com)。**