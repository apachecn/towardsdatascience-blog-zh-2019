# 卡反人类卡代(略 NSFW)

> 原文：<https://towardsdatascience.com/cards-against-humanity-card-generation-slightly-nsfw-a9c132d88345?source=collection_archive---------18----------------------->

## 出于最愚蠢的原因使用 Char-RNNs

(警告:《反人类纸牌》是一款成人主题游戏，包含大量粗鲁语言。这篇文章不会展示任何图形，只有文字，但它仍然会让你在工作场所看起来很奇怪)

![](img/77f1a893533dc236bc501634704af6b4.png)

什么是幽默？人工智能能理解是什么让事情变得有趣吗？写一篇中等的帖子能验证你花在训练电脑说脏话上的时间吗？

今天我不会回答这些问题。但希望我们都能从“人工智能”生成的 CAH 卡片中获得一点乐趣，并更深入地了解是什么让这项任务变得特别困难。

首先，我要说的是，我并没有在这里开创新的领域。文本生成已经有一段时间了，而且是由比我聪明得多的人完成的。所以我不会试图详细解释我在这里使用的深度学习方法。如果你和我一样是深度学习的书呆子，我就只说模型结构是*嵌入- > LSTM- >脱落- >稠密(char list 的长度)。*

这项任务有一些具有挑战性的部分，所以我将在下面给出一个简短的解释。如果你只是想看我制作的卡片，请随意往下跳。

![](img/b296997e9947c03f389c21a6fb65a566.png)

# 数据问题和我为什么作弊

任何深度学习项目的第一步都是找到数据。谢天谢地，一群疯狂的人已经花时间为每张 CAH 卡片创建了一个[电子表格](https://docs.google.com/spreadsheets/d/1lsy7lIwBe-DWOi2PALZPf5DgXHx9MEvKfRw1GaWQkzg/edit#gid=2018240023)，包括由第三方创建的自定义扩展。这意味着我可以只使用大约 2k 的官方白色卡片来训练模型，或者使用另外大约 19k 的第三方白色卡片。我使用白色卡片是因为有更多的例子可以训练，但是我保证当模型试图创建黑色卡片时，会给你一种感觉。

所有这些漂亮数据的问题在于，它们极其多样化。在其核心，深度学习是训练一个程序来识别模式，在这种情况下，复制它们。创建一个生成[莎士比亚剧本](https://www.google.com/search?rlz=1C1CHBF_enUS797US797&ei=rxLaXKDWNMuG0wKYyqCADA&q=generating+shakespeare+scripts&oq=generating+shakespeare+scripts&gs_l=psy-ab.3..35i39.2541.7996..8499...2.0..0.92.1075.14......0....1..gws-wiz.......0j0i13j0i13i30j35i304i39.5znL9r5jSWo)的模型很容易，因为莎士比亚有一致的声音，谈论相对相似的内容。虽然 CAH 确实有独特的声音，但它没有一致的内容。当引入第三方卡时，清晰的声音变得模糊。

这样想吧，你在学习一门新的语言，我给你两段阅读。其中一个是简短的电影评论，另一个是一系列不相关的短句，当与其他看不见的句子搭配时，这些短句旨在让该文化的人们发笑。如果我让你翻译两个，你觉得哪个会更容易？我认为是前者，因为当你不知道一个单词的意思时，你可以依靠它周围的上下文来帮助你。

由于这种多样化数据的挑战，我不得不作弊一点。我不是直接把神经网络的输出加入到生成的卡片列表中。在卡片上做了一点后期处理，并通过人工选择来剔除那些显然毫无意义的卡片。我意识到这是作弊，但请把这个系统更多地视为一个“卡片创意生成器”。不过，我也会向您展示一些原始输出。

在网络产生潜在的卡片后，我让它们通过文本处理器，检查它们与我的数据集中的卡片的相似性。相似的卡片是不可避免的，但我正试图消除那些与数据库中的卡片没有明显区别的卡片。一点必要的过度拟合也意味着网络偶尔会产生一张它看到的卡片的精确副本。

然后我用自动拼写校正器检查这些卡片。这修复了网络造成的小拼写错误，并且仍然是完全自动的，所以在我看来这是一个公平的游戏。完成后，我选择最好的卡片，并将它们添加到我的生成卡片列表中。

# S 怎么把牌给我！

![](img/2dc67d953b6ee0a339bd2a35d3d1ad44.png)

下面是我挑选的 50 张白色卡片:

*   永远好色
*   一堆辛勤工作的结肠染色的狗屎
*   一门无意的感情科学
*   大浴室
*   低矮的树枝
*   太迟了
*   被毛
*   白布丁
*   偷偷挠肉
*   一个死了的大胖妓女
*   同性恋
*   试图用一个大的便便手指做爱
*   独角兽棍子
*   不是瑕疵
*   军事决策
*   忘记至上的观念。
*   恶霸保险杠
*   一堆惊喜性爱录像带。
*   干燥的医用润滑油
*   近乎不恰当的交往。
*   你妈妈的迷恋对象。
*   一个在吸管杯中的男人
*   好盒子
*   好色的白人正义。
*   打嗝的芭蕾舞演员
*   让面包变红的孩子。
*   感觉特朗普的网站。
*   小丑公鸡。
*   去猴子酒吧
*   不是武器。
*   一个 6 岁的保姆。
*   我地下室里的节流孔
*   一系列破旧的卡片
*   悲伤的阴茎。
*   爸爸的搞笑婊子。
*   我旅行后的避孕套。
*   忍受学校
*   抱着妈妈
*   只是想交流的性阴道
*   几块有酒脑的木板
*   膨胀的大小。
*   奶奶训练。
*   唱着“哦，坦南巴娜娜”
*   69%的人
*   只是一个爱心包
*   手指婊子
*   可悲的标准
*   在世界之巅购买处女
*   油炸的东西
*   抱歉。

有意义的卡片代表了网络产生的结果的三分之一。诚然，上面的一些卡片没有意义，但一些有意义的卡片很无聊，有趣的是创造一些无意义的卡片。

下面是我的网络的原始输出(稍微格式化但未修改)的样子:

```
penis.
a shit-to-fie
the contraction of a burrito.
the ring my slowl sorr that tells you with the chinese dogs.	public motherwease.		
female social suberious with forgetting to parol into a petrodomined body show.		
an erection that lasts for hours.		
aming down on a game of minivan		
the poor		
a female orgasm		
subway shaving a single panties.		
a keyback horse with a tremendous dingus.		
an 80-year-old girlfriend		
a burger silence		
recaulation	
zego for one		
magic human remains for your secret school.		inappropriate labor.		
having sex with a dead baby fetus.		
(rangta butt pullting people.		
being kernels for domester of the mongrey.	
a flamboyant man that fires a smiling prince.		
a valladian memo baby.		
idiots		
a somen sort of this with the color off the side to.		spending the nuit as every day		
smelling sex lives of sexual charases.		
getting tape on it.		
a doctor with a sopping wet vagina.		
a fairy food.		
making up for your home.		
incurable some sexy tantrum.		
buffalo big destroying pop
```

如果你玩 CAH，你可能会认识一些。“鸡鸡”、“傻逼”、“穷人”都是直接抄牌。而“女性高潮”只是对“女性高潮”这张牌的一个小小的修改。这是网络记忆一些卡片，然后把它们吐出来。这就是为什么我在接受这些卡之前，会分析它们与数据库中其他卡的相似性。

![](img/801cad33d170412d35f15be0234e90b5.png)

Average number of words in a card was 4.94

你还会注意到，我在上面贴的白色卡片列表中几乎没有更长的卡片了。原始输出应该会告诉您原因。网络无法学会将更长的有意义的句子串在一起。我认为这主要是因为数据集中长卡片的数量很少。

## 黑卡(准备一些垃圾)

![](img/aab4b0a0c84eda335e40fcd04701094e.png)

*   每个成功的男人都是 _ _ _ _ _ _ _ _ _ _。
*   没有人认为我是一个强大的愿望与 __。
*   蛋头舞是你被难民恐怖分子杀死的机会。
*   新的早晨，有 _______ 和 ______。
*   ______ 的声音有什么用。
*   醒来时我丈夫会说 _ _ _ _ _ _ _ _ _
*   我就知道我们会是对的！
*   接下来人们发明了 ______。
*   我上一份工作中臭名昭著的一面是 ________。
*   _______ 是我生命中的一个明确标志。

我可以继续说下去，但很明显，即使是最优秀的黑牌例子也没有什么意义。它们也更容易从网络试图记忆的卡片中获得。

同样，这里有一个网络原始输出的例子:

```
nothing is better the good of death?		
check out my new podcast about ______ and ______.		
ted cruz caused a still want of ______.		
the red room for eating ____ for a kirld and gentler ______.		the probilew recommend a trip was completely ruined by ______.		___________. a wedding is a the face.		
on cheeristed ______ for his/her dont combrate your signessant-class impressed the only acceptable to have ____ in public.		
g go goage ______.		
______ is a sure sign of my life.		
snatch and ______.		
what's the biggest source of tenish in the charge of ______.		what do you were a parent when i never have to be a proctive in raid of ______.		
momes, my imanager compaint for ______.		
i wonder if ______ was all over the poil.		
immers is now explore the honors using lose in the country black, ive had a horrible vision, father. i saw mountains crumbling, stars falling from _____.		
there can a parent that did you have a moment to talk to my kids and do with ______.		
i got have ______.
```

# 结论时间

总的来说，我认为这个项目是一个有点有趣的失败。白色卡片通常很有趣，但让我想起了一个小测验，你可以用你的姓和名的第一个字母来创造你的“妓女名”或其他什么。它只是把单词拼凑在一起，并希望它是有趣的。我们甚至不要谈论黑卡。显然需要更多的例子。

我猜一个更接近“最先进”的网络可能会做得更好(没有狗屎)，但我不确定它会更好。我认为它会产生更一致、更少抄袭的结果，但它的笑话可能不会更好。问题是，为了做出好的原创卡，你必须意识到你周围的文化和事物。像这样的网络只知道已经创建的卡。

我能想到的解决这个问题的唯一方法是，在许多主题的更广泛的文本数据库上训练一个更先进的网络，然后专门让它完成生成卡片的任务。但如何做到这一点目前超出了我的能力。

如果你有任何想法如何做到这一点，或者只是更好的方法来完成这项任务，请让我知道。我很想听听你的反馈。如果你有这个帖子，我也很乐意收到反馈。我还在学习写这些文章，我可以使用一些建设性的批评。

[链接到卡片组(仅限白卡)](https://azala.info/static/index.html?deck=46622)