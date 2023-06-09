# 人工智能地牢 2 的创造者如何使用 GPT 2 来创建永无止境的冒险游戏

> 原文：<https://towardsdatascience.com/the-creator-of-ai-dungeon-2-shares-gpt-2-finetuning-advice-e5800df407c9?source=collection_archive---------11----------------------->

## 想象无限的电子游戏

![](img/9fe35013114cef1a57e8bcb05a2724a5.png)

The TI-99/4A computer I used to play text-based adventure games. (Credit: Rama & Musée Bolo on [Wikipedia](https://en.wikipedia.org/wiki/Texas_Instruments_TI-99/4A#/media/File:TI99-IMG_7132.jpg))

小时候，我在家里的 TI-82 上用盒式磁带数据驱动器玩基于文本的冒险游戏。我对斯科特·亚当斯的经典[海盗冒险](https://en.wikipedia.org/wiki/Pirate_Adventure)游戏记忆犹新，这是一款早期基于文本的视频游戏。

游戏很简单。你首先站在伦敦的一套公寓里，必须通过键入简单的命令，如“向西”、“爬楼梯”或“帮助”，导航到一个神秘的岛屿当你输入“拿朗姆酒”时，游戏回应道:“有一种奇怪的声音……我想是我。嘻嘻。”)

回到那些美好的旧时光，我不断地陷入早期基于文本的游戏的叙事约束。“我不知道那是什么”和“我不能朝那个方向走”这两句话至今仍萦绕着我，追寻着由人类作家创造和编码的想象世界的艰难界限。

![](img/74369c75500cf5e35be7b5a0c25e1e6d.png)

The old-school Pirate Adventure text-based adventure emulated on the [Frotz app](https://davidgriffith.gitlab.io/frotz/).

# 见见 AI 地牢 2 的创作者

游戏创作者 [Nick Walton](https://twitter.com/nickwalton00) 上周发布了 AI Dungeon 2，使用 OpenAI 的超能力 GPT-2 语言模型的完整 1.5B 参数版本来构建一个无限的基于文本的幻想游戏。

在 AI 地下城 2 中，我扮演了一个探索危险法术库的巫师，然后我的女儿扮演了一个保护她的城堡免受兽人入侵的贵妇。

游戏从来没有告诉我们“我不知道那是什么”和“我不能朝那个方向走。”感谢强大的 GPT 2 故事引擎，AI 地下城 2 总是试图生成一个新的场景或新的对话，不管我们的请求有多奇怪。

就我个人而言，我非常喜欢魔法书和魔法图书馆。所以我花了很长时间躲在一个废弃的城堡里看书。

![](img/deea3677d27a4bc1a8fa056cff074483.png)

A few paragraphs from one of my AI Dungeon 2 adventures.

目前，你可以在这个 Google Colab 链接上玩游戏[。](https://colab.research.google.com/github/nickwalton/AIDungeon/blob/master/AIDungeon_2.ipynb)

正如尼克在网站上解释的那样，游戏正在转型，因为他要应对“疯狂的下载费用”，这迫使他寻求一种新的发行模式:

> “我们使用 bittorrent 作为临时解决方案来托管游戏文件并保持游戏的活力。速度不快，但这是我们目前最好的了。如果你想帮忙，你能做的最好的事情就是 [**下载这个带有游戏文件**](https://github.com/nickwalton/AIDungeon/files/3935881/model_v5.torrent.zip) 和**的种子文件**尽你所能无限期地下载。这将有助于新玩家更快地下载这款游戏，并发现 AIDungeon2 的广阔世界！”

我和尼克讨论了《人工智能地下城 2》这个无尽的人工智能生成的游戏世界背后的硬件、数据集和编程。

自从我们的采访之后，Nick [更新了他的 Patreon 页面](https://www.patreon.com/posts/roadmap-32316007),更新了关于即将推出的付费订阅模式的应用版本的消息。

> *“该应用的 alpha 版本正在运行，我们拥有在云上运行该模型的基础设施。在开始测试之前，我们还需要一两天的测试，但我们希望在本周末开始。”*

这是我们关于游戏采访的完整文本…

# 创建您的训练数据集需要多长时间？

数据集是大约 30 MB 的文本冒险故事，我是从 chooseyourstory.com 的[网上搜集来的。我大概花了 20 个小时左右来构建 web scraper，运行它并管理数据集。我想确保我使用的所有数据都是正确的格式。](http://chooseyourstory.com/)

我的建议是，尤其是在文本中，少量的高质量数据比大量的低质量数据更有价值。

# 在 GPT-2 产生的故事中，你采取了哪些编码步骤来维护上下文？

我使用了一个包含 8 个高性能图形处理器的 [DGX 1](https://www.nvidia.com/en-us/data-center/dgx-1/) 来训练。我最终使用的模型花了大约 12-16 个小时来训练。

我已经尝试了很长时间，尝试了很多东西。

对正确的文本冒险数据进行微调可能是我为保持叙述清晰所做的最重要的事情。

增加内存也有所帮助。在过去，记忆更接近于 2(最后 2 个动作-结果对)，上下文句子更重要，而现在记忆设置为 10，我不确定它是否真的重要。

我也做了相当多的工作来修改玩家的输入，使其符合正确的格式，并删除模型输出，使其不包含动作线(用“>”符号表示)

# 您还修改了您的模型，以减少 GPT-2 输出中的重复。你能解释一下吗？

在 [Salesforce CTRL 模型](https://blog.einstein.ai/introducing-a-conditional-transformer-language-model-for-controllable-generation/)中，他们给生成一个已经生成的单词的概率加上一个惩罚，将它的对数概率除以大约 1.2。

这有助于避免模型陷入说同一个单词或一组单词的困境。正因为如此，CTRL 模型能够使用比 GPT-2 低得多的温度(后者需要高温来防止重复)。通过给 GPT-2 增加这个惩罚，我能够将温度降低到 0.4，这有助于连贯性，同时仍然避免重复(大部分)

# 关于你的游戏和你的微调模型所产生的故事，你对版权和知识产权有什么看法？

就像人类从其他作者那里学到了很多如何写作的知识一样，我很乐意让模特在其他人的作品上接受训练，以学习如何写得更好。就一个模型输出的东西而言，我不反对人们用它来写奇幻小说或在网上发布他们的冒险经历。

人工智能地牢 2 不是一个讲故事的人。人们发布的故事很有趣，不仅仅是因为人工智能，还因为人类如何与它互动，以创造有趣和有趣的故事。

# 您希望在未来的迭代中向数据集添加什么类型或其他格式？

我当然想加入更多的类型，但我下一步要做的是得到一个更好的主机解决方案，并完成我的反向人工智能地下城模式，其中人工智能是玩家，人类是地下城主。

![](img/1f8e91a097b3a5540680db6d38ecbd13.png)