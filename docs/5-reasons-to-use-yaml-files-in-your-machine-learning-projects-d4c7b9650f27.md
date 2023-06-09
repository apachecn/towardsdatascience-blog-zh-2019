# 在你的机器学习项目中使用 YAML 文件的 5 个理由

> 原文：<https://towardsdatascience.com/5-reasons-to-use-yaml-files-in-your-machine-learning-projects-d4c7b9650f27?source=collection_archive---------7----------------------->

## 即使你的项目很小，YAML 文件也能增加它的灵活性和可重用性。

![](img/6000210a362f8914f1059a84cd6196cb.png)

Photo by [Max Nelson](https://unsplash.com/@maxcodes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我攻读数据科学硕士期间，没有人告诉我配置文件的必要性，以及有了它们我的生活会变得多么简单。老实说，没有人告诉我作为一名数据科学家的许多非常重要的方面，我严重缺乏关于最佳实践的知识。然而，我已经在上一篇文章的[中解决了大部分问题，我不会再重复了。](/what-my-data-science-degree-did-not-teach-me-part-1-3d7ff23875e5)

[](/what-my-data-science-degree-did-not-teach-me-part-1-3d7ff23875e5) [## 我的数据科学学位没有教会我什么—第 1 部分

### &在开始我的数据科学职业生涯之前，我想知道些什么。

towardsdatascience.com](/what-my-data-science-degree-did-not-teach-me-part-1-3d7ff23875e5) 

简而言之，当我毕业的时候，我的项目有点又快又脏。它们起作用了，有时有很好的结果，但是在我的解决方案的开发过程中，灵活性和可重用性显然不是优先考虑的。项目进行的时间越长，我就越渴望找到一种方法来轻松运行项目的不同部分，重用代码或简单地定制我的环境，而不会因为想到我必须复制或重写的大量代码而感到难过。

# 什么是 YAML？

缩写 YAML 用来代表另一种标记语言。它现在代表 YAML 标记语言，以便更好地代表 YAML 目前拥有的面向数据的目的。

YAML 是一个[人类友好的数据序列化标准](https://yaml.org/)，它遵循 Python 缩进，是一个 JSON 超集。YAML 不是唯一可用于配置文件的格式；配置文件可以在中创建。JSON 或 INI 格式的 py 文件。我选择 YAML 是因为它的简单，但我稍后会回到它，因为我在这篇文章中的一个(或两个)原因是基于它的简单(剧透警告！).

## 如果您不知道什么是配置文件:

配置文件用于存储配置参数，即应用程序的初始参数和设置。这里的“应用”一词有其更广泛的定义。如果您的代码对数据做了一些事情，它符合应用程序定义。如果您想要一种简单的方法来理解配置文件的用途之一，请考虑您可能在项目中硬编码的所有内容，例如(但不仅限于！):

*   输入或输出文件位置
*   机器学习模型的参数输入
*   预处理的参数(例如，大小训练与测试集)
*   日志文件的位置

# 1.即使在小项目中，潦草地修改代码来改变参数也不是一件有趣的事情。

毫无疑问，我通常可以从项目一开始就使用 YAML 文件，但是我经常跳过这一步。我后来总是意识到，不早点用 config.yaml 开始是一个错误。不幸的是，了解最佳实践并不总是意味着我愿意自动应用它们。

任何可以在我的脚本中硬编码的东西，都可以在配置文件中占据它应有的位置。虽然您可能经常只从一个数据源开始，但大多数项目可能会变得更加复杂，从配置文件开始比以后设置要容易得多。

配置文件不仅有助于避免脚本中的硬编码路径。每当我看到自己一次又一次地修改部分代码以查看对输出的影响，或者注释掉代码以避免每次都运行一个步骤时，我(应该)意识到这部分代码或这个参数代表了在我的配置文件中设置的完美候选。我将在本文后面详述这些功能。

# 2.写你的第一个 YAML 文件是小菜一碟

YAML 文件最好的部分是简单的语法和创建一个容易。这是我在任何(机器学习与否)项目中选择 YAML 文件而不是任何其他类型的配置文件的主要原因。如果我们想给 config.yaml 文件一个输入和输出位置，那么它应该是这样的:

```
files:
   location: 'C/Users/Yourname/Mydocuments/theinputlocation.txt'
   output: 'C/Users/Yourname/Mydocuments/theoutputlocation.txt'
```

很简单，对吧？但是这里有几个特征可以让它变得更简单！

*   我也可以写一个不带引号的字符串(只要它不包含任何可能被视为 YAML 语法的特殊字符)！如果我真的想或者需要使用引号，单引号和双引号都可以。

```
files:
   location: C/Users/Yourname/Mydocuments/theinputlocation.txt
   output: C/Users/Yourname/Mydocuments/theoutputlocation.txt
```

*   YAML 使用注释的方式与 Python 等其他语言一样，使用#注释掉其余的行。

```
files:
#put the locations of your files here
   location: 'C/Users/Yourname/Mydocuments/theinputlocation.txt'
   output: 'C/Users/Yourname/Mydocuments/theoutputlocation.ext'
```

*   不需要特别的陈述，你直接从你的 YAML 文件的内容开始。

在这第二个原因上加了子原因，我有点作弊，但是如果我们可以把列表放在列表里，我肯定可以把原因放在原因里。

# 3.用 Python 阅读 YAML 文件也非常容易

因此如果编写。yaml 文件这么容易，那么读取 yaml 文件并告诉 Python 如何处理其内容呢？

```
pip install pyyaml
```

**用 Python 读 YAML 文件只需要一个包。**

下面的代码允许您正确、安全地加载。yaml 文件，如果您弄乱了您的配置文件，将返回一个清晰的错误消息。

```
import yaml
try: 
    with open (path_to_yaml, 'r') as file:
    config = yaml.safe_load(file)
except Exception as e:
    print('Error reading the config file')
```

以我们上面使用的输入位置和输出位置为例，下面是我如何访问我的设置:

```
location_input = config['files']['location']
location_output = config['files']['output']
```

*   如果您不想每次都写文件，该怎么办？

你的 YAML 档案里应该有什么:

```
write_file: True #turn to False to prevent from running
```

python 代码中应该包含什么(假设您的数据位于 pandas 数据框架中):

```
if config['write_file']:
    mydf.to_csv(location_output)
```

# 4.当你与人们分享你的应用程序时，他们(不管是不是开发人员)会喜欢你的

如果您需要共享您的程序，而人们有不同的文件存放位置，会发生什么情况？尽管大多数数据科学家&分析师喜欢通读 Python 代码，但他们会非常感激您没有强迫他们滚动每个脚本来找出在哪里更改输入/输出文件路径。

**如果整个数据科学项目需要转移到服务器上，该怎么办？**如果您只需要从项目中的一个位置导入一个文件(这种情况很少发生在我身上)，这可能不是一个问题。如果您需要从几个位置导入几个文件(并且文件有时可能会更改名称)，该怎么办？任何运行代码或从您的 g it 存储库中提取代码的人都必须仔细检查代码，找到每一条路径，并用自己的路径替换它。

此外，让人们运行您的代码来更改参数并不总是一个好主意。**限制只能访问 YAML 文件**也有助于限制对代码的损害，同时保持项目的灵活性。

# 5.它可以帮助您专注于您的机器学习代码(或项目的任何其他部分)

我目前参与的项目需要大量的代码、大量的文件加载和大量的处理。对我们来说，在每次运行整个项目来测试代码的时候开发它是不可想象的。使用 YAML 文件(或另一个配置文件)允许我们以模块化的方式建立我们的项目。

当我们回想机器学习时，大多数项目都需要昂贵的数据清理。一旦您的数据被清除，您可能不需要重新运行每个步骤。当然，Jupyter Notebook 也允许你分别运行我的代码的不同部分。但是老实说，我不止一次因为愚蠢的无限循环、沉重的模型或者我永远不会知道的非常模糊的原因而使内核崩溃。每个人都崩溃了一个内核，并对整个体验和重新运行整个代码感到不安。

例如，您可以在预处理步骤结束时将清理后的数据帧保存在一个. csv 文件中，这样您就可以仅在必要时运行这些步骤。

```
steps:
   preprocessing: False
   machinelearningstep: Truetemp_location: mytempfile.csv
```

以及它在 Python 中的样子:

```
if config['preprocessing']:
    #do extensive cleaning on my dataframe
else:
    #load the temp file that is being saved each time I run 
    #the preprocessing step in the location indicated in the config
    #file
```

YAML 文件有优点也有局限性，就像任何语言或格式的配置文件一样。我意识到我给出的许多理由也适用于另一种类型的配置文件(我第二喜欢的是. py 文件)。无论我的同事或我选择 YAML 档案或。py 文件并不重要，但是从长远来看，以一种简单、易读、友好的方式构建项目对于团队的生产力和快乐非常重要。如果从长远来看，我们可以避免挫折，为什么不呢？

[](/mindfulness-for-programmers-da6f92147b8f) [## 程序员的正念

### 编程时 3 个简单的练习

towardsdatascience.com](/mindfulness-for-programmers-da6f92147b8f) [](/explaining-data-science-to-your-grandma-f8345621483d) [## 向你的祖母解释数据科学

### 或者如何向你的家人或任何与技术世界脱节的人解释数据科学。

towardsdatascience.com](/explaining-data-science-to-your-grandma-f8345621483d)