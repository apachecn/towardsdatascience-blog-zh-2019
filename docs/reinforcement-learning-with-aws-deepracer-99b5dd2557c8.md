# 用 AWS DeepRacer 进行强化学习

> 原文：<https://towardsdatascience.com/reinforcement-learning-with-aws-deepracer-99b5dd2557c8?source=collection_archive---------19----------------------->

## 从玩具车到 AlphaGo 和自动特斯拉

2016 年 3 月，过去十年最伟大的围棋选手李·塞多尔(Lee Sedol)被 [**AlphaGo**](https://deepmind.com/research/case-studies/alphago-the-story-so-far) 以 4 比 1 击败。计算机以前在国际象棋上击败过最好的人类，但是围棋在复杂性上又上了一个台阶。你知道更疯狂的是什么吗*？这台机器在比赛前 8 小时才学会如何玩。*

*今年 2019 年 1 月，谷歌 DeepMind 团队将 AlphaGo 带到了另一个高度，制作了 [**AlphaStar**](https://deepmind.com/blog/article/alphastar-mastering-real-time-strategy-game-starcraft-ii) 。星际争霸是最复杂的视频游戏之一，它从来没有被电脑掌握过🤖以前，直到现在。AlphaStar 淘汰了两名世界级选手，以 5 比 0 击败了他们。*

*就在上个月，OpenAI(前 Elon Musk's)发布了 [**多智能体捉迷藏**](https://openai.com/blog/emergent-tool-use/) ，一个双方，寻找者和隐藏者之间的模拟。隐藏者必须避开视线👁在一个有墙、盒子和斜坡的世界里。出现了大量的策略，包括建造庇护所和箱子冲浪！查看下面的视频，了解更多信息👇*

*OpenAI’s video on their Multi-Agent Hide and Seek Simulation*

*最后但同样重要的是，就在两周前，OpenAI 发布了另一个惊人的结果，它训练了一只成功的机器人手[](https://openai.com/blog/solving-rubiks-cube/)**解魔方。它不仅能在 60%的时间里用一只手解决不同大小的 3x3 魔方，还能在有干扰的情况下解决问题(比如被一只毛绒长颈鹿推来推去)🦒 ).***

***所有这些惊人的突破有什么共同点？他们都使用目前超级热的**强化学习(RL)** 🔥机器学习领域。在高层次上，RL 涉及到一个演员在某个环境中通过*试错*来学习做什么。它被机器人、自动驾驶汽车甚至股市预测者雇佣来安全驾驶并给出准确的预测！***

***说到自动驾驶汽车，亚马逊网络服务(AWS)最近创建了一个名为[**AWS DeepRacer**](https://aws.amazon.com/deepracer/)**的挑战🚗，主要目的是向开发人员介绍 RL。通过训练一辆汽车在赛道上行驶，参赛者比赛以达到最快的时间。我决定参加他们的挑战以及相应的 [Udacity](https://www.udacity.com/aws-deepracer-scholarship) 课程，以更深入地了解 RL，我愿意与你分享它们！😃*****

# *****更深入地了解 RL*****

*****本质上，强化学习是模仿现实世界，在进化中，以及人们如何👦和动物🐶学习。通过经验，我们人类学会了在不同的情况下做什么和不做什么，并将其应用到我们自己的生活中。RL 以同样的方式通过模拟体验来帮助机器学习。*****

*****让我们以 AWS DeepRacer 为例，通过描述一些*关键术语*来描述这个问题:*****

*   *******代理/参与者:**在环境中执行动作的实体(AWS DeepRacer 和控制它的模型)*****
*   *******动作:******代理可以做什么(汽车可以转弯、加速等)*********
*   *********环境:**代理存在的地方(轨迹)*******
*   *******状态:**给定时间内的关键特征(轨道上的位置)*****
*   *******奖励:**根据代理在前一状态中的动作给予代理的反馈(做得好的奖励高，做得差的奖励低)*****

*****下面是一个基本的 RL 模型是如何学习的:一个环境中的代理在其给定的状态下执行一个动作。环境给了代理一个奖励💸这取决于其行动的质量。然后代理执行另一个操作，循环继续。一个**训练集**由一定数量动作的整个循环组成。*****

*****让我们更深入地研究一下奖励吧！*****

## *****奖励里有什么？*****

*****奖励函数是 RL 模型中非常重要的一部分。对于一个训练有素的代理人来说，拥有一个激励最佳行为并抑制不良行为的机制是至关重要的。*****

*****在 AWS DeepRacer 中，我们创建了奖励函数💰用**输入参数**。这些包括汽车的位置、离中心的距离等等。下面是一个基本奖励函数的例子:*****

*****![](img/e3acbae661d13bf9285fd90c37b4cb77.png)*****

*****Image by author*****

*****在该函数中，我们使用输入参数 *params['track_width']* 和*params[' distance _ from _ center ']*。我们创建了三个标记，并将赛车与中心线的距离与这些标记进行比较。如果汽车与中心的距离在 10%以内，它会得到 1 的奖励😊。如果在 25%以内，则给予 0.5 的奖励。如果在轨道上，它得到 0.1。如果偏离了轨道，我们给它 0.001，基本上等于零😢*****

*****![](img/37223fa68eaa86e6d3d07408ddc3a535.png)*****

*****Image by author*****

*****这个奖励功能会给坚持在赛道中间的车很高的奖励。知道了这一点，就会避免脱轨，这就是我们想要的！虽然这个奖励函数没有针对速度进行优化，但至少我们可以放心，我们可能会完成比赛。😅*****

## *****调谐超参数*****

*****让我们讨论超参数:我们可以调整或“调整”的模型设置。通过在训练前调整超参数，我们可以尝试提高模型的性能💯。以下是我们可以调整的一些超参数的示例:*****

*   *******学习速率**:模型学习的速度。如果学习率高，它学得快但可能达不到最佳状态。如果太低，可能需要很长时间训练。*****
*   *******贴现因子:**模型考虑未来的程度。如果更高，DeepRacer 就越看重未来，对考虑到未来的行动给予更高的奖励。如果低，DeepRacer 会以短期的方式思考。*****
*   *******熵:**不确定的程度。较高的值允许模型更彻底地探索环境，而较低的值允许模型利用它已经知道的东西。*****
*   *****还有更多！*****

*****有很多方法可以调整超参数，但没有正确的方法，只能通过实验来实现🔬🧪and 试错法。*****

# *****培训和评估我们的模型*****

*****现在你已经知道了 AWS DeepRacer 的强化学习，让我们来训练和评估我们的虚拟模型吧！以下是步骤(注意，您可以通过创建一个 AWS 帐户来遵循这里的[和](https://console.aws.amazon.com/deepracer/home?region=us-east-1#models)):*****

1.  *****在 AWS DeepRacer 控制台中创建一个模型。*****
2.  *****设置名称、描述和轨道。*****
3.  *****设置您的行动空间(模型可能采取的行动)。*****
4.  *****创建你的奖励函数。*****
5.  *****设置你的超参数。*****
6.  *****开始训练！*****

*****在训练过程中，您的模型将按照您指定的时间⌚在虚拟赛道上进行训练，从一个状态转换到另一个状态，并在途中获得奖励。*****

*****![](img/f85302e9a81bc269432b40be7aa7c679.png)*****

*****The training dashboard for AWS DeepRacer, including training stats and a video stream; image by author*****

*****训练结束后，在任何赛道上对模型进行评估，看看效果如何。如果它表现良好，提交到排行榜🥇！如果没有，试着改变你的奖励函数和超参数，看看你能如何改进。毕竟，这是一个反复的过程😁*****

# *****我们能从 AWS DeepRacer 身上学到什么？*****

*****我希望你在训练你的模型和在赛道上比赛时玩得开心！尽管与我们在 OpenAI 或谷歌的 DeepMind 上看到的相比，这是一个简单得多的模型，但我们仍然可以得出一些有价值的结论🔑*****

1.  *****训练一个好的模型需要大量的时间、资源和实验。想想 DeepMind 花了多少时间训练 AlphaStar！这是一个真正的迭代过程。*****
2.  *******设定一个最优的奖励函数至关重要**。没有一个好的奖励函数，模型就不能正确地学习它的任务。如果一辆车没有动力留在赛道上，你可以指望它会很快崩溃。*****
3.  *******强化学习正在掀起波澜。** AWS 让任何有资源的人都可以非常容易地拥有一个真正好的 RL 模型。我们已经看到了过去几个月的疯狂进步；想象一下我们将来会看到什么！*****

*****在 RL 领域有超级有趣的工作正在进行，你应该**兴奋**！不知不觉中，你就再也不能开自己的车了😏*****

*****![](img/1e9d8e641e628b379139ac069de39efe.png)*****

*****Photo by [Bram Van Oost](https://unsplash.com/@ort?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)*****

*****希望你喜欢阅读 RL！我也将很快在 NLP 中做更深入的探索，所以一定要关注我并在 LinkedIn 上联系我！如果你想联系我，在 albertlai631@outlook.com 给我发信息。很想聊聊:)*****

*****祝您愉快，敬请期待更多精彩！👋*****