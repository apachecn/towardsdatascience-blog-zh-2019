# 多语言机器学习

> 原文：<https://towardsdatascience.com/multilingual-machine-learning-972de4248218?source=collection_archive---------25----------------------->

## 利用专利数据探索 BLEU 评分

# 介绍

Does your machine learn in Chinese? I don’t speak Mandarin or Cantonese so Google Translate gets all the credit — good or bad — for translating the preceding sentence into “您的機器學習中文嗎?” But how might a researcher quickly evaluate the quality of machine translations? This question encapsulates the basic challenge that gives rise to the BLEU metric. BLEU, which stands for bilingual language understudy, is a default measure of machine translation quality and is also sometimes applied to [cross-lingual](https://arxiv.org/abs/1901.07291) natural language processing (NLP) tasks. The metric is well-established in the machine translation space but some analysts question the algorithm’s applicability to a wider set of tasks beyond the measure’s original objectives. This article takes an initial dive into the lessons, implementations, and limits of BLEU using examples drawn from multilingual patent documents.

# BLEU 的基础知识

IBM 的研究人员在 2002 年开发了 BLEU 算法，作为一种参考基准人工翻译来评估机器翻译质量的有效方法。如果你对该算法的创建背景和目标感兴趣，由开发人员 Papineni 及其同事撰写的原始[论文](https://www.aclweb.org/anthology/P02-1040.pdf)是一个不错的起点。BLEU 是“候选”机器翻译和一个或多个“参考”人工翻译之间匹配单词序列的调整后的精度度量。BLEU 计算机器翻译中与人工翻译中的 n-grams 匹配的长度为 *n* 的单词序列的“n-grams”，除以机器翻译中 n-grams 的总数。该度量被调整，因为它将匹配计数削减到人工翻译中 n 元语法出现的最大数量，并且还惩罚在单词长度上偏离参考翻译的机器翻译。

得到的 BLEU 分数是一个介于 0 和 1 之间的数字，其中 0 表示候选文本和参考文本之间的 n 元语法匹配为零，1 可能等于与参考文本之一完全相似的机器翻译。在实践中，通过相应 n-gram 计算的几何平均值，测量计数在多个单词序列长度上匹配 n-gram(四单词序列)、tri-gram(三单词序列)、n-gram(两单词序列)和 n-gram(一单词序列)。该算法设计用于句子语料库级别的比较，在句子的基本单元计算 n-gram 匹配，然后组合成语料库级别的分数。为了澄清术语，本文中使用的术语“文档”是指句子的语料库。如果你对理解算法的其他资源感兴趣，你可以查看 deeplearning.ai 上讨论算法细节的[视频教程](https://www.youtube.com/watch?v=DejHQYAGb7Q)，或者 machinelearningmastery.com 上探索 NLTK 实现的书面[教程](https://machinelearningmastery.com/calculate-bleu-score-for-text-python/)。为了探索度量的实际用例，我接下来使用中文专利的翻译来应用 BLEU。

# BLEU 在专利文本中的应用

## 获取翻译

根据管理专利的全球组织 WIPO(世界知识产权组织)最近的一份报告，机器学习领域越来越多的专利是用中文撰写和提交的。要在这个多语言空间探索 BLEU 的基础，你可以首先从电子商务公司阿里巴巴将其扩展到全球覆盖的一项 NLP 创新的中国国内专利开始。中文专利的标题如下所示。关于示例专利的其他细节，

```
**original_title_cn** = "机器处理及文本纠错方法和装置、计算设备以及存储介质"
```

WIPO 的数据查询工具提供了[英文](https://patentscope.wipo.int/search/en/detail.jsf?docId=WO2019085779)和[中文](https://patentscope.wipo.int/search/zh/detail.jsf?docId=WO2019085779)两种语言版本，你可以在浏览器中查看。

人类专家经常翻译出质量相当的译文，但在选词和结构上有所不同。因此，BLEU 接受单个或多个人工翻译作为比较的参考。为了更直接地探索参考译文的产生，我通过基于网络的人工翻译平台 [Gengo](https://gengo.com/) 从两个不同的人工译者那里获得了中文专利的两个汉英翻译。接下来，您可以从两个来源获得“候选”机器翻译

```
**reference_human1_summary** = "The invention discloses a machine processing and text error correction method and device, a computing device, and a storage medium, specifically comprising corrected and rewritten text pairs of incorrect text and corresponding correct text. The corrected and rewritten text pairs serving as a training corpus to train the machine processing model, thereby preparing a machine processing model suitable for text error correction. Through extraction of corrected and rewritten text pairs from a log, the machine processing model can be trained and thus made fit for text correction by inputting the first text into the machine processing model to get the second text, that is the error correction result text. In addition, the language model or the common lexicon can be used to determine whether the first text needs to be corrected. The training corpus extracted from a log can be used to train the language model, or the common lexicon can be sorted by segmenting and counting text in the log. This is how to easily implement text error correction."**reference_human2_summary = "**This invention makes public a machine processing and text error correction method and hardware, computing equipment and storage medium, and specifically pairs error text with the corresponding corrected and modified correct text. It uses this text pair as training material for the machine processing model, and from there prepares the machine processing model that is applied to the text correction. It can train the machine processing model using a diary or daily journal and make it suitable for text correction. The first text version is inputted into the machine processing model to get the second text version, which is the corrected text. Additionally, it can also use a stored language model or common vocabulary bank to determine if the first text version needs correction. It can use the practice language material gathered from the diary or daily journal to train the language model, and it can also initialize the common vocabulary bank through the segmentation and analysis of the diary or daily journal text. Through all this, text correction is conveniently implemented."
```

单独的机器学习算法，谷歌翻译和世界知识产权组织(WIPO)，如下图所示。

```
**candidate_google_summary** = "The invention discloses a machine processing and text error correction method and device, a computing device and a storage medium, and particularly comprises an error correction rewriting pair of an error text and a corresponding correct text, and an error correction rewriting pair as a training corpus, and a machine processing model. Training is performed, thereby preparing a machine processing model suitable for text correction. The machine processing model can be trained to mine the error correction by mining the error correction rewrite pair from the log. The first text is input into the machine processing model to obtain a second text, that is, an error correction result text. In addition, you can use the language model or common lexicon to determine whether the first text needs to be corrected. The language model can be trained using the training corpus extracted from the log, or the common lexicon can be organized by segmenting and counting the text in the log. Thereby, text correction is facilitated."**candidate_wipo_summary** = "The present invention discloses a machine processing and text correction method and device, computing equipment and a storage medium. Specifically comprising corrected and rewritten text pairs of incorrect text and corresponding correct text, the corrected and rewritten text pairs serving as a training corpus for training a machine processing model, and in this way developing a machine processing model for use in text correction. Through extraction of corrected and rewritten text pairs from a log, the machine processing model can be trained and thus made fit for text correction by inputting a first text into the machine processing model to obtain a second text i.e. a corrected text result. Moreover, a language model or a lexicon of commonly used words can be used to assess whether text needs correction. The training corpus extracted from the log can be used to train the language model and also, through text segmentation and statistical analysis of text in the log compile a lexicon of commonly used words. Thus, text correction can be made easier and more convenient."
```

## 计算 BLEU 分数

BLEU 有多种实现和扩展，比如流行的 [sacreBLEU](https://github.com/mjpost/sacreBLEU) 包等等。本示例首先使用自然语言工具包(NLTK)中的 [bleu_score 模块](https://www.nltk.org/api/nltk.translate.html?highlight=bleu#module-nltk.translate.bleu_score)计算分数，该工具包基于 Papineni 等人的原始实现。`corpus_bleu`函数接受表示为单个单词标记的引用和候选翻译，您可以通过标准的 NLP 预处理步骤创建这些单词标记。对于包含多个句子的文档，最初的 BLEU 实现逐句计算 n-gram 匹配，然后对所有候选句子的裁剪 n-gram 计数求和，最后除以文档中候选 n-gram 的数量。正如 NLTK 文档所述:BLEU 度量“计算微观平均精度(即在除法之前对每个假设参考对的分子和分母求和)。”默认情况下，`corpus_bleu`计算等权重 n 元语法分数的几何平均值，包括四元语法、三元语法、二元语法和一元语法。

两个机器翻译示例的 BLEU 分数计算结果是什么？结果表明，Google 和 WIPO 的翻译与 Gengo 上人工翻译的参考译文具有相似的质量。Google Translate 的第一候选译文得分为 0.53，WIPO 得分为 0.54，如下图所示。

```
# calculate BLEU score of Google translation
bleu_google = round(corpus_bleu(refs_list_6, can_google_summary[:]),         
                    2)# calculate BLEU score of WIPO translation
bleu_wipo = round(corpus_bleu(refs_list_5, can_wipo_summary[:]), 2)print(f"Google Translate BLEU score: {bleu_google}")
print(f"WIPO BLEU score: {bleu_wipo}")
```

记住这个 BLEU 应用的实际例子，有助于建立该算法对机器翻译和自然语言处理任务的应用的潜在范围。

# 蓝色界限

研究者普遍认为 BLEU 有利于机器翻译系统的评估。然而，一些研究人员警告说，BLEU 可能不适合机器翻译的某些方面或更广泛的 NLP 任务。一个关键的批评是，BLEU 分数可能不一定与人类翻译中的重大质量差异相关联。正如 Callison-Burch 和他的同事在一篇被大量引用的论文中所指出的:“有些情况下，BLEU 的改进不足以反映翻译质量的真正提高，而在其他情况下，没有必要改进 BLEU 来实现翻译质量的显著提高。”这些作者还提出，BLEU 可能不适合于比较利用不同技术的机器翻译系统，检测 BLEU 没有建模的翻译方面，或者评估测试语料库中不常见的改进。

对 BLEU 进行文献综述的研究人员在最近的一篇[论文](https://www.mitpressjournals.org/doi/full/10.1162/COLI_a_00322)中指出，BLEU 与人类的相关性可能会随着被评估系统的细节、所使用的特定语料库文本以及用于人类评估的确切协议而变化。作者，Reiter 和他的同事建议，BLEU 应该通过真实世界的人类评估来评估，如 A/B 测试，以确定 BLEU 与真实世界的有效性可靠相关的环境。基于文献综述的结果，这些作者警告说，研究人员应该将 BLEU 作为系统级机器翻译的诊断方法，而不是作为测量系统输出的评估技术。随着文献表明对该测量的效用和缺点的普遍认可，一些研究人员，例如最近一篇[论文](https://arxiv.org/abs/1804.08771)的作者，专注于增加 BLEU 分数报告的清晰度。这将包括，例如，让研究人员包括预处理方案和其他标准化惯例，用于报告 BLEU 评分的实施和评分细节。这些论文中提出的观点在专利领域和不同的用例中应用和解释 BLEU 分数时需要谨慎。

# 结论

这篇文章概述了 BLEU 分数的目标、例子和限制。要在 Jupyter 笔记本中运行本文附带的完整 Python 代码，您可以前往 Github [资源库](https://github.com/glmack/multilingual_machines)进行多语言机器学习。关于我对这个领域的兴趣的更多背景，请查看我在 lee-mackey.com[的网站。随着机器学习领域的专利文档继续变得越来越多语言化，特别是来自中文专利的专利文档，本文中提出的观点有望帮助您在将该算法应用于您的特定用例时，将考虑事项浮出水面并融入上下文。如果您在 NLP 工作流中跨语言工作，了解 BLEU 的这些细节将有助于选择是否、何时以及如何在您的项目中使用该指标。](http://lee-mackey.com/)