# 数据可视化的艺术和科学

> 原文：<https://towardsdatascience.com/the-art-and-science-of-data-visualization-6f9d706d673e?source=collection_archive---------5----------------------->

## 关于如何思考和创建出色的数据可视化的全面指南。

# 数据可视化理论

数据可视化——我们的工作定义是“数据的图形化显示”——就像开车、做饭或在聚会上找乐子一样:每个人都认为自己很擅长，因为他们已经做了一段时间了。特别是对于那些从工程背景进入数据科学的人来说，数据可视化通常被视为琐碎的事情，一旦有趣的建模完成，就要匆忙向利益相关者展示。

然而，可视化往往是向决策者解释复杂问题的主要方式。对于如此多的人的日常工作如此重要的东西，数据可视化很少被直接教授，相反，新专业人员应该通过潜移默化来学习。但是这不是最好的方法。数据可视化和其他技能一样，是一种技能，即使是有经验的从业者也可以从磨练他们在该领域的技能中受益。

因此，这个简短的话题。这篇文章有点长，但是旨在给你一个全面的数据可视化概念的支持，这将使你在工作中做得更好。

我绝不打算教你如何用特定的软件制作特定的图形。我不知道什么样的软件可能适用于你未来的需求，或者当——坦率地说，谷歌存在时，你需要制定什么样的可视化——所以这不是一本有一步一步说明的食谱。这里的目标不是为您提供未来使用的食谱，而是教您什么是面粉——向您介绍有效数据可视化的基本概念和构建块。

也就是说，你可以在我的个人 GitHub 上找到构建这篇文章[的代码(作为三个 R Markdown 文件)。](https://github.com/mikemahoney218/PersonalWebsite/tree/master/content/tutorials/dataviz)

## 咒语

我尽可能地将这些基本概念归纳为四个咒语，我们将在整个课程中继续讨论。咒语是:

1.  一个好的图形讲述一个故事。
2.  一切都应该尽可能简单，但不能再简单了。
3.  使用合适的工具完成工作。
4.  墨水便宜。电子更便宜。

每个咒语作为一个部分的主题，也将贯穿始终。第一部分的主题很简单:

## 一幅好的图画讲述了一个故事

制作图形时，理解图形的用途很重要。毕竟，您通常不会制作一个完美描述您的数据的图表-现代数据集往往太大(就观察数量而言)和太宽(就变量数量而言)，无法在单个图表上描述每个数据点。相反，分析师有意识地选择可视化中包含哪些元素，以便以最有效的方式识别数据中的模式和趋势。为了做出这些决定，思考一下*为什么*和*如何制作*图形会有所帮助。

## 我们为什么要讲故事？

至于*为什么*这个问题，答案通常可以归结为两大类中的一类:

*   帮助识别数据集中的模式，或者
*   向更多的观众解释这些模式

这些是创建分别被称为*探索性*和*解释性*图形背后的基本原理。探索性图形通常是非常简单的数据图片，用于识别数据中您可能还不知道存在的模式。以一个简单的图形为例，显示了树围作为年龄的函数:

![](img/1cdb4d458cf9aef0f2adc0ee2952d94a.png)

这种可视化并不复杂——两个变量，35 个观察值，没有太多的文本——但它已经向我们展示了数据中存在的趋势。如果我们受到启发，我们可以利用这些信息开始研究树木生长随年龄变化的*原因*，现在我们已经大致了解了*树木生长如何变化。*

同时，解释性的图表都是关于*为什么*的。探索性图形首先关注的是识别模式，解释性图形的目的是解释它们为什么会发生，以及在最好的例子中，读者应该做些什么。解释性图形可以独立存在，也可以出现在一个更大的报告中，但是它们的目标是相同的:提供为什么一个模式存在的证据，并提供一个行动号召。例如，我们可以对同一个树形图进行一些编辑，以解释我们看到的模式:

![](img/64f74f5a2e5fec42883158ce411742a6.png)

我想在这里特别指出标题:“桔子树的生长在第 4 年逐渐减少。”一个好的图形讲述一个故事，记住。因此，无论你给你的图表起什么样的标题，都应该反映出这个故事的要点——像“树的直径(厘米)与年龄(天)”这样的标题不会增加任何用户不能从图表本身得到的东西。相反，只要有意义，就用你的标题来推进你的信息——否则，如果它没有增加任何新的信息，你最好把它完全删除。

这里重要的一点是，解释性图表不一定比探索性图表更精美，或者探索性图表只供分析师使用——例如，定期报告通常会使用高度精美的探索性图表来确定现有趋势，希望激发更深入的分析来确定原因。相反，要传达的信息是，了解图表的最终目的——无论它是应该首先帮助识别模式，还是解释它们是如何形成的——可以帮助您决定需要包含哪些元素来讲述您的图表旨在讲述的故事。

## 我们如何讲故事？

当考虑图形设计时，另一个重要的考虑因素是你将如何讲述你的故事，包括你将使用什么设计元素和你将显示什么数据。在决定可能的“如何”时，我首选的范式是权衡最终图形的*表现力和有效性*，正如华盛顿大学的[杰弗里·赫尔所定义的那样，赫尔写道:](https://courses.cs.washington.edu/courses/cse442/17au/lectures/CSE442-VisualEncoding.pdf)

*   **:如果语言中的句子(即可视化)表达了一组数据中的所有事实，并且仅表达了数据中的事实，则一组事实在可视化语言中是可表达的。**
*   ****有效性*** *:如果一个可视化所传达的信息比另一个可视化中的信息更容易被感知，那么这个可视化比另一个可视化更有效。**

*或者，简单来说:*

1.  **说实话，只说实话(不要撒谎，也不要因遗漏而撒谎)**
2.  **使用人们解码更好的编码(更好=更快和/或更准确)**

*当我们进入力学部分时，请记住这个概念——它应该是您在决定使用哪些元素时的主要考虑因素！在其他两节中，我们将继续回到解释性和探索性，以及表达性和有效性这些概念。*

# *数据可视化的机制*

*让我们从制图的理论考虑转移到你所拥有的实际构建模块。在这样做的同时，我们还将继续第二条箴言:*

## *一切都应该尽可能简单——但不能再简单了。*

*图表本质上是我们数据的 2D 图像:*

*![](img/a64329df8a51746773ea1a0ff80a9e20.png)*

*它们有一个 x 轴和一个 y 轴刻度，就像我们这里的散点图一样，一个点在每个刻度上的位置告诉你它的值有多大。但是这种设置只允许我们查看数据中的两个变量——我们经常对查看两个以上变量之间的关系感兴趣。*

*所以问题变成了:我们如何将这些额外的变量可视化？我们可以尝试添加另一个头寸规模:*

*![](img/efa1db3bc7f557021322c59bdb34a4d6.png)*

*但是 3D 图像很难让你理解，制作起来很复杂，在传达信息方面也不太有效。它们确实有它们的用途——尤其是当你能够构建真实的、物理的 3D 模型，而不仅仅是在 2D 平面上制作 3D 形状时——但通常不值得这么麻烦。*

*那么我们的工具箱里有什么工具呢？普遍认同的(不，真的——这是一个激烈辩论的领域)分为四类:*

*   *位置(就像我们已经有了 X 和 Y)*
*   *颜色*
*   *形状*
*   *大小*

*这些是我们可以用来在图形中编码更多信息的工具。我们将把这些称为*美学*，但是任何数量的其他词也可以使用——一些人把它们称为尺度，一些人把它们称为价值观。我称它们为美学，因为这是我选择的语言(R，使用 ggplot2)对它们的称呼——但这个词本身来自于这样一个事实，即这些是改变你的图表外观的东西。*

*值得一提的是，我们使用的是 EPA 的数据集，代表了 1999 年和 2008 年 38 种流行车型的燃油经济性数据。“Hwy”是公路里程，“displ”是发动机排量(so 体积)，“cty”是城市里程。但坦率地说，我们的数据集现在并不重要——我们这里的大部分讨论适用于您将获得的任何数据集。*

*我们将逐一介绍这些美学，讨论如何在每个图形中编码更多信息。一路上，记住我们的咒语:*

1.  *一幅好的图画讲述了一个故事*
2.  *一切都应该尽可能简单——但不能再简单了*
3.  *使用合适的工具完成工作*
4.  *墨水便宜。电子甚至更便宜*

*我们将在本节中讨论这些是如何适用的。*

## *位置*

*让我们通过结束对位置的讨论来开始讨论这些美学。值沿 x、y 轴或(在我们的 3D 图形中)z 轴的距离代表特定变量的大小。人们天生就知道每个轴上的值越靠外越极端，例如，假设您看到了下图(由模拟数据制成):*

*![](img/a1840ad25e026ae6b95db4f8e08e8fa6.png)*

*你认为哪些值更高？*

*大多数人天生认为左下角代表两个轴上的 0，离那个角越远，值就越高。这个相对明显的发现暗示了数据可视化中一个更重要的概念:[感知拓扑应该与数据拓扑](http://stat405.had.co.nz/lectures/20-effective-vis.pdf)相匹配。换句话说，这意味着图表中*觉得*大的值应该代表数据中*大的值。因此，当处理位置时，更高的值应该是离左下角更远的值——你应该让你的观众的潜意识假设为你做这些。**

*将这个建议应用于分类数据可能会有点棘手。假设我们正在查看数据集中汽车制造商的平均公路里程:*

*![](img/c08b2a10beacddffa3f4bd7e8454364c.png)*

*在这种情况下，x 轴上的位置只代表不同的汽车制造商，按字母顺序排列。但是请记住，图形中的位置是一种美学，我们可以用它在图形中编码更多的信息。我们在这里没有这样做，例如，我们可以完全不使用 x 位置来显示相同的信息:*

*![](img/8e8c484c3b316795211abfb43abe29ab.png)*

*试着比较第一张图上的庞蒂克和现代，和第二张图上的。如果有什么不同的话，去掉我们无关的 x 美学让比较制造商变得更容易。这是我们第二个口号背后的一个重要驱动力——一切都应该尽可能简单，但不能再简单了。拥有额外的美感会让一个图表变得混乱，让它更难理解它试图讲述的故事。*

*然而，当制作图形时，我们应该始终致力于使重要的比较变得容易。因此，我们应该利用我们的 x 美学，不按字母顺序排列我们的制造商，而是按他们的平均公路里程排列:*

*![](img/3a95d84106a7e7428c02f94708a48dd9.png)*

*通过重新排序我们的图形，我们现在能够更好地比较更多相似的制造商。现在理解我们的可视化要快得多——更接近的比较更容易进行，所以将更多相似的值放在一起更容易理解。例如，看看现在庞蒂克和现代的对比。一般来说，不要按字母顺序排列东西——使用你放置东西的顺序来编码附加信息。*

*顺便提一下，我个人认为，当沿着 X 轴处理分类值时，应该对值进行重新排序，使最高值排在最前面。出于某种原因，我只是发现将最高的条/最高点(或任何用来显示价值的东西)放在 Y 轴旁边看起来比另一个更整洁:*

*![](img/c18889a053d47b341ff2255b112e43d9.png)*

*值得一提的是，当值在 Y 轴上时，我不那么武断了。我个人认为最高的价值应该总是在顶部，因为人类期望更高的价值在离左下角更远的地方:*

*![](img/f77647e1c6e96ae7f606335e895169e4.png)*

*然而，我并不像在 X 轴上那样立即厌恶相反的顺序，可能是因为最下面的条/点看起来更像一个自然的形状，并且仍然沿着 X 轴线:*

*![](img/a27d3cef780b3ca677692dd84a384a03.png)*

*为此，至少你的里程可能会有所不同。此外，值得指出的是，当标签在 Y 轴上时，图表上的标签要干净得多——翻转您的坐标系，就像我们在这里所做的，是当您有大量类别时显示数据的好方法。*

## *颜色*

*虽然我们已经很好地介绍了职位在信息交流中的作用，但我们仍然停留在开始时的同一个问题上:我们如何在图表上显示第三个变量？*

*最流行的方法之一是用颜色来代表你的第三个变量。可能值得讨论一下如何将颜色用于模拟数据集。以下面的图表为例:*

*![](img/2a0ea802aba30554c19b24f6209b697f.png)*

*现在让我们为第三个变量添加颜色:*

*![](img/d60e9f06ae5cfc4243fb4149fc27a9bd.png)*

*记住:感知拓扑应该匹配数据拓扑。哪些值比较大？*

*大多数人会说是深色的。但事情总是那么简单吗？让我们改变我们的色标来比较:*

*![](img/def82f2e9a955b0777fbe2d2ce59106b.png)*

*当然，其中一些颜色比其他颜色更暗——但我不会说它们中的任何一种告诉我一个值是特别高还是特别低。*

*这是因为人类不会将*色调*——颜色的实际色调——视为有序值。一个点的颜色并不表示该点的值高于或低于图上的任何其他点。相反，色调作为一个*无序*值工作，它只告诉我们哪些点属于哪个分组。为了判断一个点的值有多高或多低，我们不得不使用*发光*——或者单个点有多亮或多暗。*

*你可以沿着另一个轴移动颜色来编码值——颜色的鲜艳程度，称为*色度*:*

*![](img/fb1d8bf658903ba4b12446faa57b543e.png)*

*请记住*亮度*和*色度*——一种颜色有多亮和有多鲜艳——是*有序值*，而*色调*(或颜色的阴影)是*无序值*这在处理分类数据时变得相关。例如，回到我们开始时的散点图:*

*![](img/64a843ca76ac9cacc674e1b5f2b467c0.png)*

*如果我们想在其中编码一个分类变量，例如，车辆的类别，我们可以使用色调来区分不同类型的汽车:*

*![](img/d5b733dafb07505ca7728171895cca86.png)*

*在这种情况下，使用色调来区分我们的变量显然比使用色度或亮度更有意义:*

*![](img/439f26aa9d308c8fada43de5f0500512.png)*

*这是一个知道使用什么工具的问题，色度和亮度将清楚地暗示某些变量比分类数据更接近，而色调不会给你的观众提供任何关于有序变量的有用信息。但是，请注意，我仍然不鼓励使用彩虹来区分图形中的类别——彩虹的颜色并不完全是无序的值(例如，红色和橙色比黄色和蓝色更相似)，并且您最终会暗示您可能不想暗示的类别之间的联系。还有，彩虹真的很丑:*

*![](img/aa7e21bbdbaeb17cce3b7d0c0ec3ca2e.png)*

*说到在工作中使用正确的工具，人们在数据可视化中最喜欢做的事情之一就是过度使用颜色。以下面的例子为例:*

*![](img/017d12f9d196bcd4e7c9f7c0945eb99b.png)*

*在该图中，变量“类”由沿 x 轴的位置和颜色表示。通过重复这项工作，我们正在使我们的图表更难理解——对信息编码一次就足够了，再编码更多次就会分散注意力。记住第二条箴言:一切都应该尽可能简单——但不能再简单了。最好的数据可视化是包含传递消息所需的所有元素，仅此而已。*

*您可以在图形中随意使用颜色，只要它能为图形添加更多信息，例如，如果它编码了第三个变量:*

*![](img/ef34c230a8b0c721fe7a795f296cab97.png)*

*但是像我们上面做的那样复制只会给你的图表增加更多的垃圾。*

*还有最后一种方法可以在你的绘图中有效地使用颜色，那就是突出具有某些特征的点:*

*![](img/4a996010706545819dcfd5b2d03d589f.png)*

*这样做可以让浏览者快速挑选出图表中最重要的部分，从而提高图表的有效性。顺便说一下，请注意，我使用形状而不是颜色来区分车辆的类别——结合点突出显示和使用颜色来区分分类变量是可行的，但也会有些混乱:*

*![](img/a3a13854b5616bb704a7c44d4ba469ad.png)*

*还有一个原因是颜色是一种微妙的美学，很难在你的图形中找到正确的颜色:大约 5%的人(10%的男性，1%的女性)根本看不到颜色。这意味着你在可视化中使用它时应该小心——使用色盲安全调色板(查看“ [ColorBrewer](http://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3) 或“ [viridis](https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html) ”了解更多这些)，尽可能与另一种美学搭配。*

## *形状*

*最容易搭配颜色的美学是第二个最常用的——形状。这个比颜色更直观，为了演示，让我们回到散点图:*

*![](img/9272a77097c595d2e2b0a515521ff577.png)*

*现在，我们可以根据每个点代表的车辆类别来改变每个点的形状:*

*![](img/e703f5aadf315897a4d53db63f65de66.png)*

*想象一下，我们正在做与之前颜色相同的练习——哪个值更大？*

*我告诉你这些形状代表什么，已经破坏了答案——它们没有一个天生比另一个大。形状和色调一样，是一个*无序值*。*

*当我们改变线的形状时，同样的基本概念也适用，不仅仅是点。例如，如果我们为前轮、后轮和四轮驱动汽车绘制单独的趋势线，我们可以使用线型来表示每种类型的车辆:*

*![](img/a692fa71aea554412ee827a48d2c5db5.png)*

*但即使在这里，没有一种线型意味着比其他线型更高或更低。*

*然而，这条规则有两点需要注意。例如，如果我们回到原来的散点图，改变我们使用的形状:*

*![](img/c508a1af7dbb99e9800ea698b1bd57a2.png)*

*该图似乎暗示了前三类汽车(都是不同类型的菱形)和接下来的三类(都是三角形)之间的更多联系，同时挑出 SUV。通过这种方式，我们能够用形状来暗示我们分组之间的联系——更多相似的形状，仅仅在角度或纹理上有所不同，意味着彼此之间的关系比其他类型的形状更密切。这可能是一种祝福，也可能是一种诅咒——例如，如果你选择一个正方形和一个菱形来代表两个不相关的群体，你的观众可能会意外地读到比你原本想暗示的更多的关系。*

*同样值得注意的是，不同的形状会很快使图表变得杂乱无章。一般来说，在一张图上使用超过 3-4 个形状是一个坏主意，超过 6 个意味着你需要思考一下你到底想让人们带走什么。*

## *大小*

*我们最后的审美是尺寸。回到我们最初的散点图，我们可以想象这样使用大小:*

*![](img/3d648f95ea60e49396fec783a85bef42.png)*

*尺寸是一个固有的*有序值* —大尺寸点意味着更大的值。具体来说，人类认为更大的区域对应更大的值——上图中三倍大的点的值也大约是三倍大。*

*如果错误地使用了大小，或者错误地使用了大小，或者扭曲了数据，这就变得棘手了。有时，分析师会将半径映射到变量，而不是点的面积，从而生成如下图:*

*![](img/b97017cbec2abfe40a61dc5fc7cb4b82.png)*

*在本例中，代表 cty 值 10 的点看起来远没有代表 30 的点大 1/3。这使得在看这个图表时增加看起来更陡峭——所以当使用尺寸作为美学时要小心，你的软件使用的是点的面积，而不是半径！*

*同样值得注意的是，与颜色不同——颜色可用于区分分组，也可用于表示有序值——使用分类变量的大小通常不是一个好主意。例如，如果我们将点大小映射到车辆类别:*

*![](img/e87f847556a7c1110d74e78a9c7102e9.png)*

*我们似乎在暗示实际上并不存在的关系，就像小型货车和中型车基本上是一样的。因此，最好仅对连续(或数字)数据使用 size。*

## *切线*

*既然我们已经讨论了这四种美学，我想快速切入正题。当谈到人类感知这些美学的速度和难易程度时，研究确定了以下顺序:*

1.  *位置*
2.  *大小*
3.  *颜色(尤其是色度和亮度)*
4.  *形状*

*正如我们反复讨论的那样，最好的数据可视化是包含与传递消息一样多的元素，而不是更多。一切都应该尽可能简单，但不能再简单了。*

*然而，我们生活在一个人类的世界里，科学上最有效的方法并不总是最受欢迎的。由于从美学角度来看，颜色本身比尺寸更令人兴奋，从业者经常发现他们自己用颜色来表示尺寸已经足够的价值。因为我们知道，颜色通常应该与形状一起使用，以便在我们的可视化中更具包容性，所以大小通常是图表中使用的最后一种美学。这很好——有时我们必须为其他事情进行优化，而不是“有人能多快理解我的图表”,例如“我的图表看起来有多吸引人”或“我的老板想从我这里得到什么”。但值得注意的是，万一你在未来看到矛盾的建议——分歧来自于你的来源是教授最科学合理的理论，还是最适用的实践。*

*让我们从美学转向我们的第三条箴言:*

## *使用合适的工具完成工作。*

*回想一下我们的第一张图表:*

*![](img/4e70ae30206a7732e63a67f4df52a1bc.png)*

*正如你已经知道的，这是一个*散点图*——也称为*点阵图*。现在假设我们添加了一条最佳拟合线:*

*![](img/6dbcf9d75f8ca9b4701d8d7ef41b41f3.png)*

*一旦我们在它上面画了一条线，它就不再是一个散点图——但是术语散点图不再真正包含这里发生的一切。这显然也不是一个折线图，因为即使它上面有一条线，它也有一些点。*

*与其对这是什么类型的图表吹毛求疵，不如描述一下我们用什么工具来描述我们的数据更有帮助。我们将这些称为*几何*，是*几何*的缩写——因为当你真正深入事物时，这些是你的数据集如何沿着图表的 x 轴和 y 轴分布的几何表示。我不想在这条路上走得太远——我只想解释一下词汇，这样我们就不会讨论那是什么类型的图表，而是讨论它使用什么几何图形。以这种方式组织事物会更容易理解事物如何组合和重新格式化，而不是假设每种图表只能做一件事。*

## *两个连续变量*

*这张图表使用了两种几何图形，非常适合具有连续 y 和连续 x 的图形，即点和线。这就是人们大多数时候所说的线形图——显示数据模式的单一平滑趋势线。然而，折线图也可以指每个点依次相连的图表:*

*![](img/83a93ab0ec49b707c4c95b5b8e7c8c06.png)*

*很重要的一点是，要清楚你期望生成哪种类型的图表！为了清晰起见，我总是把前期称为趋势线。*

*这些类型的图表对于快速探索性图形具有巨大的价值，显示变量的各种组合如何相互作用。例如，许多分析师开始使用相关矩阵(也称为散点图矩阵)来熟悉新的数据集，相关矩阵创建了一个散点图网格来表示每个变量:*

*![](img/8dcd4c0dcef8ed80a6eff7d7ee20e154.png)*

*在这种格式中，理解数据之间的交互既快又容易，某些变量的交互显然是很有希望的进一步探索的途径。*

*稍微回顾一下，在继续之前，我想强调散点图的一个主要缺点。如果您碰巧有多个点具有相同的 x 和 y 值，散点图会将每个点绘制在前一个点上，使其看起来比实际数据少。向您的值中添加一点随机噪声(例如，在 Excel 中使用 RAND())有助于显示数据的实际密度，尤其是当您处理的数字没有得到应有的精确测量时。*

*![](img/7f43bb2f1028e69735a602f5f6a531a3.png)*

*最后一个适用于两个连续变量的图表是面积图，它类似于折线图，但填充的是线下的区域:*

*![](img/66dd5400e6714ad8b13b963fd6cc49ad.png)*

*当 0 是与数据集相关的数字时，面积图是有意义的，也就是说，0 值不会特别意外。当您有多个分组并关心它们的总和时，也经常使用它们:*

*![](img/10a292897356409e1225973898167091.png)*

*(这个新的数据集是“钻石”数据集，代表 54，000 颗钻石的大小、质量、切割和销售价格。从现在开始，我们将来回使用它和 EPA 的数据集。)*

*堆积面积图的一个缺点是，由于下方所有分组的累积效应，很难估计任何单个分组如何沿 x 轴移动。例如，0.25 克拉的“普通”钻石实际上比 1.0 克拉的要少——但因为“理想”和“优质”钻石如此之多，你的观众可能会得出错误的结论。在总数比分组更重要的情况下，这是没问题的——但在其他情况下，值得看看其他类型的图表。*

## *一个连续变量*

*相反，如果您希望了解单个连续变量在整个数据集中的分布情况，那么直方图是您可以使用的最佳工具之一。直方图显示数据集中有多少观察值落在连续变量的特定范围内，并将其计数绘制成条形图:*

*![](img/ce9bbaab73c1f1534cfe40f49424251e.png)*

*直方图的一个重要标志是，您需要注意数据是如何装箱的。如果您没有为条柱选择正确的宽度，您可能会错过数据集中的波峰和波谷，并且可能会误解数据的分布方式，例如，如果我们绘制 500 个条柱，而不是上面使用的 30 个条柱，会发生什么变化:*

*![](img/ff96eb09b7e9166e0c542efa16f06e6b.png)*

*直方图的替代方法是频率图，它使用折线图代替条形图来表示数据集中某个值出现的频率:*

*![](img/7090dbd359527c431215065c02e3041e.png)*

*然而，你必须再次注意这些图表的数据仓有多宽——如果你不小心的话，你可能会不小心抹平数据中的主要模式！*

*![](img/6482c785123f3ffe65f022e7f27cde5f.png)*

*与直方图相比，频率表的一大优势是它处理多个分组的方式——如果您的分组在变量的不同级别进行支配交易，频率表将比直方图更明显地显示它们如何变化。*

*(请注意，我对数据做了一些奇怪的处理，以便显示下面的分布是如何变化的。)*

*![](img/9b4c5a46deffd3ec1a7248ea77c23529.png)*

## *一个分类变量，一个连续变量*

*如果你想比较一个分类变量和一个连续变量，你通常会被某种形式的条形图所困扰:*

*![](img/1c9a68d24277baf44ccfc52365037242.png)*

*条形图可能是现存的最不令人兴奋的图表类型，主要是因为它是如此普遍——但那是因为它真的擅长它所做的。条形图是最容易解释和最有效的可视化类型之一，无论它们多么令人兴奋。*

*然而，有些人真的打算破坏这一点。以堆积条形图为例，它通常用于添加第三个变量:*

*![](img/8dd0d8f4692ed8750a3fef757686e1ce.png)*

*比较公平/G 和优质/G。几乎不可能准确地比较这两种情况——它们没有共同的顶线或底线，所以你无法真正进行比较。在这些情况下，最好使用隐藏条形图:*

*![](img/2551d385620c72bb462fc1480fcac7bb.png)*

*在比较不同分组的实际数字时，隐藏条形图通常是更好的选择。然而，这个图表很好地显示了条形图遇到的一个限制——一旦你超过了 4 或 5 个分组，进行比较就很棘手了。在这些情况下，你可能试图应用错误的图表，应该考虑将你的图表分成更小的部分——记住，墨水很便宜，电子或者更便宜——或者用几条线代替横条。*

*然而，堆积条形图适用于比较每个条形图中两个不同组的相对比例。例如，以下面的图表为例:*

*![](img/3d4f35a44051b31d6a1d36c61b9628c4.png)*

*在这种情况下，进行组间比较是很简单的，因为所有组共享一条公共线，组 1 为 100%，组 2 为 0%。这个参考点解决了我们在两个以上分组中遇到的问题——尽管注意，如果条形图的总和不总是相同，我们仍然更喜欢一个隐藏的条形图。*

## *快速切入正题*

*这通常是大多数人对饼状图及其糟糕程度进行长篇大论的地方。他们错了，但以一种可以理解的方式。*

*人们喜欢讨厌饼图，因为它们几乎都是糟糕的图表。然而，如果对你的浏览者来说，能够快速找出两个或更多的分组在整体中所占的比例是很重要的，那么饼图实际上是表达观点的最快和最有效的方式。例如，比较以下使用相同数据集制作的饼图和条形图:*

*![](img/0a425a6dede0d2e8cb6e99af895f4077.png)**![](img/5a02bca440777eedafde96e90046020a.png)*

*比如说，在饼状图中，从 A 到 F 比从 C 到 F 更容易辨别，因为人类更擅长求和角度而不是面积。在这些情况下，请随意使用饼图——并告诉任何批评你的人，我说没问题。*

## *两个分类变量*

*我们的最后一个组合是当你在 x 轴和 y 轴上都有一个分类变量时。这些是需要考虑的更棘手的情节，因为我们不再根据一个点离左下角有多远来编码位置值，而是必须创造性地有效使用位置来编码值。请记住，geom 是数据集沿图表的 x 轴和 y 轴分布的几何表示。当你的两个坐标轴都是绝对的，你必须创造性地展示这种分布。*

*一种方法是使用密度，就像我们在散点图中所做的那样，来显示有多少数据点落入了图表中的每个类别组合中。您可以通过制作“点云”图表来实现这一点，其中更密集的云代表更常见的组合:*

*![](img/8279a0c4b47f0208cd3a1266f235b23c.png)*

*即使这张图表上没有一个数字，它的信息也很清楚——我们只需扫一眼就能知道我们的钻石是如何分布的。类似的方法是使用热图，不同颜色的单元格代表一系列值:*

*![](img/1f0e5fca622f06814be9f414d472a516.png)*

*我个人认为热图效率较低——部分是因为通过使用颜色美学来编码这个值，你不能将它用于任何其他东西——但它们通常更容易用手头的资源来制作。*

# *制作出色的可视化效果*

*当我们进入最后一节时，是时候详细说说我们最后的咒语了:*

## *墨水便宜。电子更便宜。*

## *处理大数据集*

*回想一下我们在上一节中使用的钻石数据集。它包含了 54000 颗钻石的数据，包括每颗钻石的克拉数和售价。如果我们想比较这两个连续变量，我们可能会认为散点图是一个很好的方法:*

*![](img/26e3ea5342ddf9e4c16d513e4d19febb.png)*

*不幸的是，看起来 54，000 点对这个情节来说太多了，对我们没什么好处！这是所谓的*过度绘制*的一个明显例子——我们只是在一个图表上有太多的数据。*

*这个问题有三个真正的解决方案。首先，我们可以简单地决定我们想要重构我们的图表，而不是显示一个指标——例如平均销售价格——在不同的克拉上如何变化，而不是我们的数据如何分布:*

*![](img/2680f5ab798a7488697717c7b4d2c1af.png)*

*我们有各种各样的方法来进行这种重构——如果我们愿意，我们可以通过宁滨我们的数据得到一个非常相似的图表，并制作一个柱状图:*

*![](img/15b8fea242815aa37dcce3a66cf55dc5.png)*

*然而，无论哪种方式，我们都没有真正显示出与原始图表中相同的东西——我们没有任何迹象表明我们的数据是如何沿着这两个轴分布的。*

*第二个解决方案更有效地解决了这个问题——让你的所有观点都半透明:*

*![](img/7d5de3288768318be52813f10652b1c7.png)*

*通过这样做，我们现在能够看到数据分布更加密集的区域，这是汇总统计中所没有的，例如，低克拉钻石似乎比高克拉钻石的分组更加紧密。我们还可以在克拉的“整数”值上看到一些暗条纹，这表明我们的数据存在一些完整性问题，如果鉴定师更有可能给一颗钻石一个整数的话。*

*当我们想要在图形中映射第三个变量(让我们使用 cut)时，这种方法的挑战就来了。我们可以像往常一样尝试改变图表的美感:*

*![](img/53d1be1eddfd0212c66aa00b7566c313.png)*

*但不幸的是，点的绝对数量淹没了图形上颜色和形状的大部分变化。在这种情况下，我们最好的选择可能是将我们的图分面，也就是说，将我们的一个大图分成几个小的倍数:*

*![](img/2322d67568cf29051213dbf6ee9aa70a.png)*

*墨水便宜。电子更便宜。制作多张图表。*

*通过将我们的数据分割成几个更小的图形，我们能够更好地看到分布如何在我们的类别之间转移。事实上，我们可以使用这种技术将我们的数据进一步分割成散点图矩阵，显示不同的组是如何分布的:*

*![](img/c5b141743e50e39dc64f0ba7dcffab09.png)*

*分面的最后一个非常有用的用途是用多条缠绕的线分割图表:*

*![](img/fa6e2a2e4a649745e52735e343e323f0.png)*

*这些图表通常被称为“意大利面条图”，当被分割成小的倍数时，通常更容易使用:*

*![](img/30367d2a3df8bcc397f15a400bae1425.png)*

*现在，刻面图的一个主要缺点是它们会使比较变得更加困难——如果在我们的折线图中，知道大多数净度在 2 克拉的价格上接近比知道每个净度的价格如何随克拉变化更重要，那么第一个图表可能是更有效的选择。然而，在这种情况下，重新评估你的图表上实际需要多少行是值得的——如果你只关心一些清晰度，那么只包括那些行。目标是使重要的比较变得容易，理解一些比较比另一些更重要。*

# *处理图表垃圾*

*回想一下我用作解释性图表示例的图形:*

*![](img/cc79307f47c8edb07bb0bf696a949778.png)*

*你可能已经注意到，这张图表与本课程中的所有其他图表风格不同，它没有灰色背景或网格线或其他任何东西。*

*记住我们的第二条箴言:一切都应该尽可能简单，但不要再简单了。这张图表反映了这一目标。我们已经失去了一些令人分心的元素——彩色背景和网格线——并改变了其他元素，使整个图形更加有效。我们的目标是在图表上没有无关的元素，以便尽可能地表达和有效。这通常意味着使用最少的颜色，最少的文字，没有网格线。(毕竟，这些行通常只在挑选特定值时有用——如果您希望人们需要特定值，您应该给他们一个表！)*

*那些无关的元素被称为“垃圾图表”。你在 Excel 中制作的图表中会经常看到这种情况，它们会有深色背景、深色线条、特殊的阴影效果或不编码信息的渐变，或者最糟糕的是那些“3D”条形图/折线图/饼图，因为这些东西可以通过单击来添加。然而，它们会使你的图形不那么有效，因为它们迫使用户花更多的时间将数据和装饰分开。一切都应该尽可能简单，但不要太简单——所以不要试图用无用的元素美化你的图表。*

*chartjunk 的另一个常见实例是图形中的动画。虽然动画图形令人兴奋和时尚，但它们往往会降低图形的有效性，因为作为人类，当某些东西在移动时，我们无法专注于其他任何东西。[看看这些来自哈佛视觉实验室的例子](http://visionlab.harvard.edu/silencing/)——它们展示了当动画加入时，注意到变化是多么困难。这并不是说你永远不能使用动画——但是当你的图形看起来很酷比它传达信息更重要的时候，它的使用是最好的。*

# *常见错误*

*在我们结束本课程时，我想以几个常见的错误作为结束，这些错误在其他任何部分都没有得到很好的解释——主要是因为我们太忙于谈论*良好的*设计原则。*

## *双 y 轴*

*这些错误中最主要的是带有两个 y 轴的情节，这是江湖郎中和金融顾问们自未成文的日子以来所钟爱的。有两个 y 轴的图表是一种很好的方法，可以让你的图表中不存在的相关性变得真实。几乎在每种情况下，你应该只做两个图表——墨水很便宜。电子更便宜。确切的原因不在本课的讨论范围内，[所以请点击这个链接](https://kieranhealy.org/blog/archives/2016/01/16/two-y-axes/)阅读这个主题非常有趣。下面我借用了基兰的代码——看看我们如何暗示不同的事情，只要改变我们如何缩放我们的轴！*

*![](img/701a93f09493b2b0bcafa50d3983f828.png)*

## *过于复杂的可视化*

*可视化的另一个常见问题来自于分析师对他们的图表过于技术化。例如，回想一下我们最初的钻石散点图:*

*![](img/ff16e3354784704ad2f5d2a42765e578.png)*

*看这张图表，我们可以看到克拉和价格有正相关关系——一个增加，另一个也增加。然而，这不是线性关系；相反，随着克拉数的增加，价格似乎上涨得更快。*

*更有统计学头脑的分析师可能已经在想，我们可以通过对数变换坐标轴来使这种关系呈线性——他们是对的！当我们进行转换时，我们可以看到一个清晰的线性关系:*

*![](img/599f60abd64385f87d9f5be3f5e0be56.png)*

*不幸的是，以这种方式转换你的可视化会使你的图形难以理解——事实上，只有大约 60%的专业科学家能够理解它们。因此，像这样变换轴会降低图形的有效性，这种类型的可视化应该保留给探索性的图形和建模。*

# *结论*

*这就结束了对数据可视化基本概念的介绍。希望你已经掌握了一些概念或词汇，可以帮助你在日常生活中思考你自己的形象化。如果没有别的，我希望你记得我们的数据可视化的咒语:*

1.  *一个好的图表讲述一个故事。*
2.  *一切都应该尽可能简单——但不能再简单了。*
3.  *使用合适的工具完成工作。*
4.  *墨水便宜。电子更便宜。*

*希望这些概念能帮助你最大化可视化的表现力和效率，指导你使用尽可能多的美学和设计元素来讲述你的故事。你将知道如何匹配感知和数据拓扑。你会努力让重要的比较变得简单，你会知道制作不止一个图表。*

*祝你好运。向前去想象，也教别人如何去想象。我们的领域会因此变得更好。*

**Mike Mahoney 是一名数据分析师，热衷于数据可视化和寻找将数据洞察力应用于复杂系统的方法。在他的网站上了解更多*[](https://www.mikemahoney218.com/)**或* [*在 LinkedIn 上与他联系*](https://www.linkedin.com/in/mikemahoney218/) *。***