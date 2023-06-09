# 为文本分类模型引入“香蕉测试”

> 原文：<https://towardsdatascience.com/introducing-the-banana-test-for-near-perfect-text-classification-models-ee333abfa31a?source=collection_archive---------10----------------------->

## 结合拼写纠正、术语过滤和“香蕉测试”来构建弹性文本分类模型。

![](img/870ff838b621731e231b7173c793ad8d.png)

Source: [https://pixabay.com/photos/bananas-fruits-food-grocery-store-698608/](https://pixabay.com/photos/bananas-fruits-food-grocery-store-698608/)

# 介绍

有 ***数百万*** 的实例表明，企业已经在他们的系统中收集了自由格式的文本。为了自动化利用这些数据的业务流程，自由格式的文本通常需要被划分到更高级别的类别中。文本分类模型能够快速有效地对这种自由形式的文本进行分类……在很大程度上。

不管报告的验证/测试准确性如何，有许多陷阱会导致即使是训练最良好的文本分类模型也无法进行准确的分类。特别是，文本分类模型在面对从未见过的文本时往往会失败。

如果您的目标是最大化新文本分类模型的准确性，您应该考虑使用香蕉测试。尽管名字很傻，但这是一种非常真实的技术，可以用来提高模型的质量。

# 什么是香蕉测试？

香蕉检验旨在作为一个决定因素(通常与置信区间相结合)来判断给定的分类是否可信。由于机器学习模型在默认情况下总是会对数据进行分类，并且它提供的置信区间只不过是对概率(而不是准确性)的一种度量，因此香蕉测试有助于确保模型只在有足够的训练数据来做出自信的决策时才对新数据进行分类。它是如何工作的以及它为什么重要都是非常简单的概念。

解释一下测试的名字，“香蕉”这个词从来没有和我工作过的任何公司有过关联。由于我在进入数据科学之前曾是一名产品负责人，我开始相信定义适当的验收标准对于开发一个好的产品至关重要。因此，作为正在构建的任何新文本分类模型的一种接受标准，我强制要求我的模型应该 ***从不*** 自信地对包含单词“banana”的文本字符串进行分类。

为什么不呢？嗯…

1.  一个理想的文本分类模型应该在一个巨大的文本语料库上进行训练，这个语料库包含了在生产中出现的几乎每一个术语。
2.  如果一个模型已经在一个非常大的数据堆上训练过，那么文本语料库中不存在的任何术语几乎肯定是奇怪或不寻常的。这表示术语可能与未经训练的类别、拼写错误或完全不符/错误的数据(例如，文本输入到错误的字段)相关联。
3.  为了避免错误，模型应该只在它对正在查看的数据训练有素并且对答案非常有信心时才对文本进行分类。
4.  如果一个模型从未在一个提供的文本字符串中看到一个或多个术语，那么就没有办法保证它有信心进行分类。在许多情况下，它仍然会得到正确的答案，但也有很大的机会，未经训练的术语可能会改变答案。为了追求完美，当面对从未见过的文本数据时，模型应该自我报告它不知道答案。理想情况下，模型还会对它未能识别的术语进行自我报告。

因此，香蕉测试就是将输入数据中要分类的术语列表与模型已训练的术语列表进行比较，并确定是否完全覆盖。如果有些术语不包含在定型数据中，则输入数据无法通过香蕉测试，可能不应该由模型进行分类。在 Python 中，使用集合交集(或许多其他解决方案)可以非常容易地做到这一点；具体实现看你了。

这种策略导致了精确和可靠的文本分类模型，代价是被分类记录的百分比略有降低。

# 实际例子

假设您正在训练一个 tensorflow 模型来区分啤酒和葡萄酒，输入数据以自由格式文本的形式提供。我们还假设您的模型接受最多五个术语(单词)作为基于记号化器和单词索引的填充数组。

在对一些训练数据进行预处理和标记后，您的单词索引可能看起来像这样:

```
{
    "beer": 1,
    "wine": 2,
    "pinot": 3,
    "noir": 4,
    "chardonnay": 5
    "lager": 6,
    "cabernet": 7,
    "cab": 8,
    "rose": 9,
    "ipa": 10,
    "pilsner": 11,
    "zinfandel": 12,
    "chianti": 13,
    "porter": 14,
    "stout": 15,
    "sauvignon": 16,
    "red": 17,
    "blend": 18,
    "merlot": 19,
    "ale": 20,
    "mead": 21
}
```

根据上面的单词索引…

*   如果您向模型提供文本`"pinot noir"`，那么得到的数组将是`[3, 4, 0, 0, 0]`。
*   如果您提供文本`"red blend"`，得到的数组将是`[17, 18, 0, 0, 0]`。
*   如果您提供文本`"ipa"`，得到的数组将是`[10, 0, 0, 0, 0]`。

这听起来不错。但是，您可以向这样的模型提供许多值，这会导致错误分类。例如…

*   如果您提供了文本`"banana"`，那么得到的数组将是`[0, 0, 0, 0, 0]`。这个术语根本没有出现在单词 index 中，但是数组仍然是基于用来填充输入序列的函数创建的。对于在训练数据中出现频率最高的两个类别(啤酒或葡萄酒),生成的分类将显示较高的置信区间。解决这个问题的一个办法是在分类之前把所有的空数组都踢出去，然后就到此为止，但是…
*   如果您提供了文本`"neither wine nor beer"`，那么得到的数组将是`[0, 2, 0, 1, 0]`。假设您决定剔除空数组，模型仍然会有把握地错误分类这个记录。分类的置信区间也可能出人意料地高，这取决于两个类中的每一个有多少训练数据(即，如果有 300 条关于葡萄酒的训练数据记录，而只有 20 条关于啤酒的训练数据记录，则模型可能非常确信该输入属于葡萄酒类)。
*   如果您提供文本`"this is a beer"`，得到的数组将是`[0, 0, 0, 1, 0]`。这个模型仍然可能正确地分类这个记录，但是输入可能会说`"definitely not a beer"`,结果得到的数组会是完全相同的。
*   如果您提供了文本`"bourbon"`，那么得到的数组将是`[0, 0, 0, 0, 0]`。这大概应该是一个全新的类(白酒)。

根据上面的例子，如果您的模型能够自我报告它看到了从未训练过的新术语，并避免对这些不一致的记录进行分类，这不是最好的吗？

通过在进行预测之前应用香蕉测试，您的模型将能够剔除上面的每一条记录，并提供一组未通过测试的术语，如`bourbon`、`banana`、`definitely`等。这种方法可以让你创建一个非常有意义的反馈循环。这也意味着您可以将您的模型投入生产，并且知道它只会在识别每个术语时对记录进行分类。

# 香蕉测试的先决条件

应用香蕉测试时会出现一些问题。也就是说，香蕉测试可以标记在训练过程中被过滤掉的术语和/或不能识别拼写错误的术语。

以下步骤是我认为应用香蕉测试的先决条件，这样你就可以避免这样的问题。无论您决定如何对数据进行预处理，在训练过程和分类过程中都应该应用完全相同的步骤。

## 案例规范化

在训练文本分类模型或向其输入新数据进行分类之前，您几乎应该始终将文本规范化为单个大小写(通常为小写)。我说“几乎总是”是因为我确信有一些例外，其中大小写可能对模型有意义。

## 术语过滤

术语过滤并不总是必需的，但通常是推荐的。有些术语，甚至是停用词，对于提供长短期记忆(LSTM)层这样的东西的上下文可能仍然很重要。在从文本语料库中过滤太少或太多的术语之间，你需要找到一条微妙的界限。祝你好运。

## 拼写纠正

拼写纠正有助于规范化术语的变化，以便香蕉测试(以及一般的模型)尽可能有效。我过去使用的一种方法是使用字符串距离函数将文本语料库中最常出现的术语与文本语料库中的每一个其他术语进行比较。通过基于字符串距离分数过滤结果，数据中存在的许多拼写错误将会暴露出来。这种技术需要手动检查，但如果数据中的术语/拼写错误比一般的拼写自动纠正算法能够可靠处理的要复杂一些，通常会产生很好的结果。

# 香蕉船

香蕉船是对香蕉测试的可选增强(正如你现在所知道的，我喜欢为严肃的事物取愚蠢的名字)。简单地说，香蕉分裂是在执行香蕉测试之前，从文本语料库(基于 TF/IDF)中分离出总术语的前 N %的实践。

香蕉分裂很重要，因为文本语料库中最不常用的术语可能具有最少的与之相关联的训练数据。通过将香蕉分割应用到香蕉测试的实现中，您可以控制模型在对数据进行分类时的保守程度。模型见过(但可能很少见到)的术语可以被踢出去，就好像模型以前从未见过它们一样。

# 结论

尽管名字很有趣，方法也很简单，但这种技术对于制作能够有效处理新数据且错误最少的文本分类算法来说至关重要。到目前为止，它已经帮助我和我的团队大大提高了几十个模型的准确性和可靠性，并且已经成为我们的标准做法。我希望它也能让你受益，也许有一天我会听说其他人也在使用香蕉测试！