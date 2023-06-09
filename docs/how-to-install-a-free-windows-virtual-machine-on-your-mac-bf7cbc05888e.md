# 如何在你的 Mac 上安装一个完全免费的 Windows 10 操作系统来获得乐趣和利润

> 原文：<https://towardsdatascience.com/how-to-install-a-free-windows-virtual-machine-on-your-mac-bf7cbc05888e?source=collection_archive---------0----------------------->

## 创建免费虚拟机的完整初学者指南:轻松运行任意数量的操作系统进行黑客攻击、游戏、渗透测试、软件测试、调试等等。

![](img/d15607e13518c463ccdc1dce5c1a3082.png)

Image by [Ian Lindsay](https://pixabay.com/users/IanZA-2026973/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2888519) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2888519)

你可以在你的 Mac 电脑上免费运行完全不同的操作系统。大概五分钟后就可以启动运行了。

想要一台运行 Windows 10 的机器？

**搞定。**

![](img/5b4a05e603a02eaa23294b472d870155.png)

即使是最忠实的 Mac 粉丝在某些时候也可能想要或需要使用 Windows(或另一个操作系统)。你可能想测试一些在 Windows 下运行的很酷的工具或游戏。你可能迫切需要一个不同于你面前的操作系统。你可能需要检查一些有问题的软件，或者处理一个错误或病毒。

> 有可能是你真正开始玩游戏的时候了…

GIF via [GIPHY](https://media.giphy.com/media/l0MYuRLWtpg7amOf6/giphy.gif)

幸运的是，在你的 Mac 上安装一个免费的虚拟机并像运行其他应用程序一样运行它非常简单。一旦你知道你在做什么，只需要不到五分钟的时间！

## 关于虚拟机

无论您是对渗透测试、黑客攻击、软件调试感兴趣，还是只想(或需要)运行一些基于 Windows 的程序和游戏，虚拟机(VM)都是一个方便的东西。它们允许你在桌面上的一个窗口中安装和运行操作系统，如 Windows 或 [Kali Linux](https://www.kali.org/) 。

这个新的客户操作系统认为它运行在一台真正的电脑上，但它实际上是运行在你的 Mac 上的一个软件内部。该虚拟机与您计算机的其余部分“隔离”。这意味着它完全独立于你的电脑。您可以免受 bug、病毒和许多其他安全问题的侵害。

![](img/74d374ab2ec26e6287614d7b4740fdbb.png)

Photo by [MILKOVÍ](https://unsplash.com/@milkovi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

虚拟机允许你同时运行多个操作系统。您可以在一个操作系统上运行为另一个操作系统编写的软件，而无需重启。因为您可以配置您的虚拟硬件，您甚至可以安装一个旧的操作系统，如 d OS 或 OS/2。

您可以随时用“快照”保存计算机的状态，并在需要时恢复到该状态。这让你可以自由地试验你的环境。如果出现问题，无论是软件安装还是系统感染病毒，您都可以轻松切换回之前的快照。不需要持续的备份和恢复。

## [VirtualBox](https://www.virtualbox.org/)

尽管有很多流行的虚拟机程序，但是 VirtualBox 是完全免费的，开源的，非常棒。当然，有些细节，比如 3D 图形，在 VirtualBox 上可能不如在你付费的东西上那么好。如果你追求的是速度和图形，你可能会想看看付费版本。

> 我听说 Parallels Desktop 很棒，比 VirtualBox 快得多，但我自己并没有真正试过。如果你有喜欢的，在下面的评论里让人们知道吧！

那么什么是虚拟机呢？它是一种计算机文件(通常称为图像)，其行为类似于实际的计算机。**这就像你在自己的电脑里创造了一台电脑。它运行起来很像任何其他程序，但虚拟机与系统的其余部分是分开的。这意味着虚拟机内部的软件无法逃脱并篡改你的计算机。这使得它成为测试新版本、检查受感染数据、创建操作系统备份以及在最初不支持的操作系统上运行应用程序和软件的理想场所。**

您甚至可以在同一台计算机上同时运行多个虚拟机。

![](img/bb322d63bc292875ed22a1c608809112.png)

Image by [(Joenomias) Menno de Jong](https://pixabay.com/users/Joenomias-2512814/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3295891) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3295891)

## 我想要那个

我们将对安装带有扩展包的 VirtualBox 并运行 Windows 10 所需的绝对基础知识做一个简单的演练。这只是设置的一种方式。如果你感兴趣的话，你可以从这里得到更多的乐趣！

我们将要使用的程序是完全免费的，我们有使用它们的许可。(我把它放在这里是因为当你接近黑客世界时，事情会变得相当棘手。)我们将前往 Oracle 获取 VirtualBox 和 VirtualBox 扩展包。然后我们将前往[微软](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)获取我们想要使用的 Windows 版本。

## 步骤 1:下载 VirtualBox

如果你进入 [VirtualBox](https://www.virtualbox.org/) ，你会看到一个巨大的绿色“下载 VirtualBox”按钮。继续点击或者前往 [VirtualBox 下载页面](https://www.virtualbox.org/wiki/Downloads)为您的系统选择正确的 VirtualBox 版本。如果你在 Mac 上，你会点击 MacOsX 链接。

![](img/39f7ab28353c35f6e834b4107c8740e0.png)

或者:

![](img/fb5e8d19ca30df62f4d68e4043662bc2.png)

在下载页面上，您还会看到一个标题为“VirtualBox 6 . 0 . 8 Oracle VM Virtual Box 扩展包”的部分单击“所有支持的平台”下载扩展包。

![](img/9d396f70aefe1049107df166743318e1.png)

## 第二步:抢到 Windows 10

你有几种方法可以在你的虚拟机上安装 Windows 10，但这是我发现的最简单的一种。它是由微软专门为测试目的而设计和发布的。如果您想要运行 Windows 10 和“选择平台”下的“VirtualBox”，请确保您选择了“MSEdge on Win10 (x64) Stable 1809”然后点击“下载。拉链"按钮！

> *****更新* * *这是一个完全免费的 Windows 10 版本，但是你并没有无限制、不受限制地使用这个软件。**这不是你可以永远无限制使用的无限制版 Windows。我不知道你在哪里可以找到这样的东西，但是如果你有，请告诉我们！
> 
> 该软件由微软提供，仅供有限使用。该许可证的有效期为 90 天。你可以复制一份，用它来重新安装软件，90 天后就没问题了(这在[官方文件](https://az792536.vo.msecnd.net/vms/release_notes_license_terms_8_1_15.pdf)中有明确说明)。如果你想在 90 天后继续使用该软件，请为此制作一份副本)，但这不是完全版的 Windows 10，它可以永远免费使用，没有任何限制。这是微软提供的 Windows 10 的合法免费版本，您可以在有限的时间内用于有限的目的，并随时从网站或备份副本快速轻松地重新安装。
> 
> 当然，这并不是在 VirtualBox 上安装 Windows 10 的唯一方式。对于初学者和开发人员来说，这是一种非常快速和方便的方式来访问和测试 Windows 10 所提供的大部分功能。
> 
> [请参考官方文件进行澄清](https://az792536.vo.msecnd.net/vms/release_notes_license_terms_8_1_15.pdf)。

![](img/13a4c1f48d6dca2f4f82b82c1a98005e.png)

## 有些可选:取消归档

下载[解压器](https://theunarchiver.com/)也是有意义的。这是打开这些文件的快速、免费和强大的方法。在[微软官方文档](https://az792536.vo.msecnd.net/vms/release_notes_license_terms_8_1_15.pdf)中也有推荐。你不需要使用它来打开 VirtualBox 或扩展包，但使用像这样的应用程序来提取 Windows 10 下载是一个好主意。

![](img/d36a0f23efbfd69d584492e6ab8ed531.png)

一旦你的下载准备好了，去你的下载文件夹。右键单击 VirtualBox 图标，转到“打开方式”，然后单击“取消归档”这将解压缩并打开您的文件。

![](img/fb27d59178079c0a0655eddadc238562.png)

## 步骤 3:安装 VirtualBox 和扩展包

您可以像安装任何程序或应用程序一样，直接将 VirtualBox 安装到应用程序文件夹中。当然，如果你想的话，你可以改变位置。然后按照安装程序的提示进行操作。

接下来，转到您的应用程序文件夹(或您为 VirtualBox 指定的位置),双击图标将其打开。

您可以像安装 VirtualBox 一样打开并安装您的扩展包。当您开始安装时，您会看到一个弹出窗口，让您知道您正在安装什么。点击“安装”

![](img/c511d815cca8b5a00075937891411332.png)

## 步骤 4:启动并运行您的操作系统

现在您已经安装了 VirtualBox，是时候创建虚拟机了。要做到这一点，你需要一个操作系统。我们将使用我们的 Windows 10 微软下载，但如果你进入这个，你有很多选择！

继续使用解压缩程序打开您的 Microsoft 下载。如果您想按原样使用，Windows 已经安装完毕，可以随时运行。为此，请单击“导入”您可以按原样导入它，然后随时修改您的设置。如果你没有不同的计划，就按现在的方式导入吧。

![](img/290d9ab6ad02456c33bb17c4450817ba.png)

现在转到 VirtualBox 并单击“新建”这将打开一个向导，引导您完成安装。

首先，你需要给你的虚拟机一个名字。因为这很有趣，所以我强烈建议给你的虚拟机取一个描述性强、简单明了的名字。过一段时间后，他们开始看起来非常相似，这将为你节省一些严重的挫折。类似“Windows 10”或“MSEdge-Win10”的东西很有意义。

如果你选择了有创意的名字，并真正进入其中，你可能很难记住“松饼”运行的是 Windows 10，而“Tchotchke”运行的是 [Kali Linux](https://www.kali.org/) 等等。

![](img/9941952fb0194dc17b138dd2de75b452.png)

Image by [MrsBrown](https://pixabay.com/users/MrsBrown-692504/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1543541) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1543541)

指定您将运行的操作系统的类型(Microsoft Windows)和版本(Windows 10 64 位)，然后单击“下一步”

![](img/94709a98aaacde83b14bd29dd138e6ca.png)

现在你需要设置内存的大小。您正在指定有多少计算机内存将分配给虚拟机。VirtualBox 会自动让您知道所选操作系统的建议最小容量，但您可以根据需要增加或减少。

请记住，您只能使用系统实际拥有的内存量，将其设置为最大值并不是一个好主意。当您运行虚拟机时，将不会有任何空间留给您的常规操作系统使用！不要指定超出您能力范围的内容，尤其是当您认为可能会同时运行多个虚拟机时。不管怎样，你最好待在绿色区域。否则，您可能会面临一些严重的性能问题。

![](img/6ce170cad6d6b0f4794927ca8ac40d93.png)

点击“继续”

现在你需要创建一个虚拟硬盘。选择一个选项并单击“创建”，然后浏览提示并再次单击“创建”。你需要一个虚拟硬盘来安装你的操作系统和其他程序。

虚拟硬盘最常见的格式是 VirtualBox 磁盘映像(VDI)。确保它至少有足够的空间来安装操作系统。请记住，您要安装的任何程序也会占用您的虚拟硬盘空间！

> 我选择了“动态分配”作为存储细节，但这可能不适合您。一个**动态分配的文件**会随着你存储数据而增长。它开始很小，但它会成长。另一方面，**固定大小的文件**将立即占据您指定的大小。尽管这种类型的文件最初会占用更多的空间，但它会产生较少的开销。这意味着它实际上稍微快一点。

单击“创建”创建您的新虚拟机！现在你会看到你的新机器列在你的 VirtualBox 窗口的左侧。

![](img/34813451c5b47bef1971200a9ecfb5a4.png)

是时候开始操作系统安装了！配置好虚拟机后，安装向导将关闭，您将返回 VirtualBox 主窗口。双击左边的新机器(或者确保它已被选中，然后单击“开始”)。

要从映像文件(这就是我们有的)安装，请单击文件夹图标浏览您的文件。你正在寻找我们的微软下载。选择该文件并单击“开始”

现在您的安装将开始！一旦完成，你就可以开始了。

## 恭喜你！

你现在是一台运行在你的 Mac 上的 Windows 机器的骄傲的主人了！

![](img/a2145ce6e030595f6a7ff2f676a63ffa.png)

在你设置的时候，确保你把你的虚拟机当成一台完全独立的计算机。这会帮助你避免沮丧。当你运行你的虚拟机时，它完全独立于你的真实计算机。您无权访问相同的文件和文件夹。即使你点击鼠标也不会在你的电脑和虚拟机之间来回移动，除非你这样设置。

## 最终细节

双击 VirtualBox 屏幕左侧的机器，或者在任何想要运行机器的时候单击机器并点击“开始”。

![](img/9e331ea595739896b455e3924fc9f837.png)

将会打开一个窗口，您将会看到全新的 Windows 机器。真正启动并运行可能需要几秒钟(或几分钟)。如果一开始感觉有点慢或者有故障，深呼吸几次。

一旦你的新 Windows 机器开始运行，继续点击窗口中的任何地方来唤醒它。它会要求您输入用户名和密码。你可以在[官方安装文档](https://az792536.vo.msecnd.net/vms/release_notes_license_terms_8_1_15.pdf)中随时找到这些。(你的用户名是“IEUser”，密码是“Passw0rd！”但是你可以在控制面板的“用户帐户”下随时更改)

![](img/06e717d0024feaca3cc555613897b978.png)

当你第一次启动你的机器时，窗口非常小。您可以按正常方式扩展窗口，但它不太可能会调整大小以适应最初的大小。你可以通过从视图菜单中选择“缩放模式”来实现。如果您想忽略纵横比，请在调整窗口大小时按住 shift 键。

首先，当你在虚拟机上工作时，它会“拥有”你的键盘和鼠标。您可以在窗口的右下角看到从虚拟机切换到常规操作系统所需的命令。在虚拟机运行时，您还可以选择在两者之间来回移动鼠标，方法是转到屏幕顶部的**输入**并选择“鼠标集成”

## 移动文件

在设置好我的虚拟机后，我需要快速抓取一些我下载到 Mac 上的文件和程序。这是一个小紧急情况，没有时间进行研究。这可能不是将您的信息从 Mac 转移到 Windows 机器的最佳方式(反之亦然)，但我发现将我的文件上传到 OneDrive 是从 Mac 上获取我需要的内容的最简单、最快的方法。它已经安装好了，可以在 Windows 机器上运行了。注册 OneDrive 既快又免费。

这肯定不是唯一的解决方案，但如果你很着急，它就在这里。(如果你目前没有存储问题，Dropbox 也可以工作得很好……)

## 快照

VirtualBox 允许您复制虚拟机的确切状态。允许你在任何时候回到那个状态。这对于测试软件或其他配置非常有用。您可以通过点按“机器”菜单并选择“拍摄快照”来拍摄快照该快照将被添加到 VirtualBox 菜单左侧的虚拟机列表中。您可以通过右键单击快照并选择“恢复”来恢复快照恢复快照时，自创建快照以来对虚拟硬盘所做的任何更改都将丢失。

## 停工

关闭虚拟机时，您有几个不同的选项。每一种对机器的影响都有所不同。当您关闭虚拟机窗口时，您会看到几个选项。您可以选择:

*   **保存机器状态。**这将虚拟机保存为您关闭时的状态。您正在运行的任何程序都将保存为其当前状态，当您再次启动机器时，一切都将恢复。
*   **发出关机信号。**这将向虚拟机发送一个关机信号，它将像你按下物理计算机上的电源按钮一样关机。
*   **关闭机器电源。**这将关闭机器的电源，就像切断了计算机的电源一样。什么都不会被保存。

![](img/9dae20de16deffa5d0b5568d03781c83.png)

## 你做到了！

恭喜你！！！你现在是一台免费 Windows 机器的骄傲拥有者，你可以在你的 Mac 上随时运行它！在这里你几乎可以做任何事情。开始玩吧！

和往常一样，如果你用这些信息做了什么惊人的事情，请在下面的评论中让每个人都知道，或者随时在 LinkedIn [@annebonnerdata](https://www.linkedin.com/in/annebonnerdata/) 上联系。

感谢阅读！如果你想接触或找到更多酷的文章，请来和我一起在[内容简单](https://contentsimplicity.com/articles/)！

[![](img/cdeab18f634f5a92932a1c1d7bad812a.png)](https://contentsimplicity.com/articles/)