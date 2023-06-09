# 为视频和图像构建快速面部识别

> 原文：<https://towardsdatascience.com/building-fast-facial-recognition-for-videos-and-images-7b9f3e7c240c?source=collection_archive---------6----------------------->

## noobs :D 面部识别入门

在我开始这个故事之前，我要对 PyImageSearch 的 Adrian 大声喊一声。如果您是深度学习的初学者，这是市场上最好的课程。(我会把他的页面链接在底部。)

如果你和我一样是科幻迷，你应该看过《感兴趣的人》。你已经看到人工智能在视频中寻找人脸。它从图像库中找到人脸。这是电视版。如果我告诉你你也可以在现实生活中建造。我暂时忘记了那件事。

关于这个项目，我从几天前认识的室友那里得到了灵感。他一直向朋友们问我角色名字。不如我们在视频中建立面部识别系统。艾利安的代码让这一切成为可能。

想法很简单，CNN 提供足够多的图片。我从朋友那里为 5 个角色输入了 15 张图片。可以从面部识别中获取面部识别编码，存储在 pickle 文件中。您可以再次读取此编码，并与图像和视频文件中的人脸进行匹配。如果匹配，它将抛出我们存储在程序中的 known_name。如果没有找到，它将抛出未知。

我会为谷歌图片添加 github 回购和 scrapper 代码。Recog.py 文件包含 pickle 文件中的编码示例。将使用这个 pickle 文件。Recog_faces 将使用 pickle 文件，该文件在下面提到的截图中使用。如果文件不在数据集中，它将抛出未知的矩形。对每个字符使用最大数量的样本，这样我们可以有大量的编码。这将有助于面部识别。我们同样可以在视频中进行人脸识别。

## 提到的例子的小代码指南。

[https://gist.github.com/saurabh896/b705536ba4354c8aa382978d5ddfc8e4](https://gist.github.com/saurabh896/b705536ba4354c8aa382978d5ddfc8e4)

这个代码的主要部分是面部识别。我们使用相同部分的代码来转储 pickle 文件中的编码。就像我说的，更多的样本会提供更多的准确性。我用每个字符 15 个样本来运行这个代码，所以我达到了大约 83%的准确率。你仍然可以看到模型不能识别瑞秋的脸。上面的代码可以识别图像中的人脸，并将编码保存在数组中。如果你想查看编码，只需打印编码和已知人脸。你会得到看起来像坐标的人脸数据点。如果你想试试，你可以做到。**记住数据科学领域是由好奇心推动的。**

[https://gist.github.com/saurabh896/ffdc37836684420491cab60a01982658](https://gist.github.com/saurabh896/ffdc37836684420491cab60a01982658)

上面的代码改变你的阅读你的图像。打开你的 pickle 文件，循环你的编码。使用图像中提供的面孔查找匹配的编码。如果匹配，它将从编码数组中抛出名字。如果找不到脸，那么它将给出未知。

[https://gist.github.com/saurabh896/4ee6e4bfe24467df535f7762b8b112e2](https://gist.github.com/saurabh896/4ee6e4bfe24467df535f7762b8b112e2)

视频的最后代码。视频只不过是根据时间排列的图像。因此，我们一帧一帧地分割图像，并像处理图像一样对它们进行匹配。我们使用两个部分首先是输入作为输入视频，其中包含这个字符和输出文件夹，以获得矩形有界输出的模型。

如果你想了解更多关于 imutils .使用以下链接

[](https://www.programcreek.com/python/example/93641/imutils.video) [## imutils.video Python 示例

### 本页提供 imutils.video 的 Python 代码示例。

www.programcreek.com](https://www.programcreek.com/python/example/93641/imutils.video) 

这段代码需要时间，因为它正在写入新文件。我更喜欢使用笔记本电脑，因为它有很好的配置。如果你没有好的系统，使用自动气象站或 GCP 进行实验。

![](img/0695e0184d3e1a1bf55a6d9cd112b1a2.png)

Facial recognition on characters

我在视频中实现了相同的 pickle 文件。这给了我以下结果。我不得不调整一些代码来处理慢动作，但最终想法奏效了！！瑞秋出了点小问题。希望詹妮弗·安妮斯顿不会介意！！:P

Video Example

你可以在 github repo 中找到工作代码。我提到了向下看，如果你有兴趣的话。很高兴从你这里得到更多的想法。

给我打 saurabhkdm721@gmail.com 的电话

[](https://github.com/saurabh896/VideoRecognition.git) [## saurabh 896/视频识别

### 此时您不能执行该操作。您已使用另一个标签页或窗口登录。您已在另一个选项卡中注销，或者…

github.com](https://github.com/saurabh896/VideoRecognition.git) [](https://www.pyimagesearch.com/) [## PyImageSearch——擅长 OpenCV、Python、深度学习和计算机视觉

### 这篇 OpenCV、深度学习和 Python 博客是由 Adrian Rosebrock 撰写的。精通 OpenCV，深度学习，Python，还有…

www.pyimagesearch.com](https://www.pyimagesearch.com/)