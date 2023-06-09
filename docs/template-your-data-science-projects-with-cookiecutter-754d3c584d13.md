# 使用 cookiecutter 模板化您的数据科学项目

> 原文：<https://towardsdatascience.com/template-your-data-science-projects-with-cookiecutter-754d3c584d13?source=collection_archive---------13----------------------->

![](img/5e999461751206d2a507b5c8624fbb30.png)

Photo by [Neven Krcmarek](https://unsplash.com/@nevenkrcmarek?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在工作和生活中，每个人都必须完成重复的任务。说到数据和分析，例如，您可能在包含相同代码集的同一个笔记本上使用了相同的文件夹结构来分析不同的数据集。在这种情况下，人们所做的就是复制和粘贴他们的文件夹，然后手动更改他们的代码输入，希望不会在途中忘记任何东西，或者在执行这种令人生畏和讨厌的任务时分心。

有一个强大的工具可以避免以上所有情况，那就是 [cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) ！这是为您知道需要重复多次的分析类型创建项目模板的一种不可思议的方式，同时只需输入一次必要的数据和/或参数。我将在这篇博文中介绍的例子非常琐碎，但是要记住，其目的是为了理解 cookiecutter 是如何工作的。一旦做到了这一点，你只需要变得有创造性，并适应你的需求！

> 注意:如果您想使用 cookiecutter，它必须是您的环境的一部分。如果您使用 Anaconda，在您的终端中键入`conda list`,看看它是否出现在安装包列表中，否则只需键入`pip install cookiecutter`

假设我想创建一个文件夹模板(一个包含笔记本，另一个包含我需要保存的文件)，我想让笔记本在数据帧上执行某种计算。下面的快照显示了我每次运行 cookiecutter 时想要复制的结构。

![](img/68c06b02284661b99ea5120a4e646e0e.png)

该笔记本的目的是创建一个可定制行数和列数的数据框架。dataframe 将用两个值之间的整数填充，这两个值每次都可以改变。该模板还允许我选择我想要在行(或列)上运行的 numpy 函数，并将结果存储到将保存在 deliverables 文件夹中的文件中。当然，每次我想创建一个包含这样一个项目的文件夹时，我希望能够输入这样一个文件夹的标题，以及我要保存的文件的名称。该模板包含奇怪的语法，如`{{cookiecutter.folder_title}}`，其中`folder_title`是 json 文件中包含的可定制变量之一。请记住，每次克隆模板时，包含在双花括号中的所有变量(在笔记本中，以及文件夹的名称)都将被替换为 json 文件中传递的相应值。

所有这些信息都进入`cookiecutter.json`文件，该文件中的**必须保存在模板文件夹**、**、**的顶层，如上图所示。

# 填充`cookiecutter.json`

json 文件是一个字典，包含了我每次创建这类项目的新副本时想要更改的变量的所有默认值。

# 创建模板笔记本

在模板笔记本中编写您想要复制的代码，并使用我上面提到的符号来分配变量，如下面的代码行所示:

为了更好地了解正在发生的事情，可以在[这个链接](https://github.com/emmagrimaldi/cookiecutter_example/blob/master/%7B%7Bcookiecutter.folder_title%7D%7D/notebook/Cookiecutter_example.ipynb)找到整个笔记本。

# 无需再复制和粘贴，即可继续您的项目！

好的，太好了！现在是时候使用这个了，但是…我如何在每次克隆我的模板时改变我输入的值呢？轻松点。

从你的终端，移动到你想要克隆项目的文件夹，输入`cookiecutter <absolute_path_of_Cookiecutter_folder>`。一旦您这样做了，终端将要求您输入 json 文件中包含的所有变量的值，一次一个。如果您没有输入任何内容就按 enter 键，cookiecutter 将使用 json 文件中的默认值。完成后，瞧，项目的副本就创建好了！您将看到衍生和笔记本文件夹出现在您的当前目录及其所有内容！您现在可以打开笔记本并按原样运行它了！

这是一个很难解释的话题，不是因为它很难，而是因为它做起来比描述起来容易得多。出于这个原因，我把这个例子放在了我的 GitHub 页面上，这样你就可以克隆它并试用它了！玩了一会儿之后，你就会明白这有多强大，并且有望让你的(分析)生活变得更容易，这取决于你的需求！

![](img/e617ba7ebe3f3cc33ed5ad510738322e.png)

请随意查看:

[本帖的 GitHub repo](https://github.com/emmagrimaldi/cookiecutter_example)。

[我的其他中帖。](https://medium.com/@emmagrimaldi)

[我的 LinkedIn 个人资料。](https://www.linkedin.com/in/emmagrimaldi/)

**感谢您的阅读！**