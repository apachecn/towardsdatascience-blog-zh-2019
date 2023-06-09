# 爱丽丝医生和云原生鲍勃，我最喜欢的机器学习用户

> 原文：<https://towardsdatascience.com/doctor-alice-and-cloud-native-bob-my-favorite-machine-learning-users-5c2b36998e0d?source=collection_archive---------17----------------------->

爱丽丝和鲍勃都很棒，这也很好，因为我无论走到哪里都会遇到他们！他们热情、勤奋，尽最大努力构建伟大的机器学习解决方案。不幸的是，很多事情阻碍了他们，让他们慢了下来。

我的工作是倾听并帮助所有的 Alices 和 bob:)在这篇文章中，我将尝试总结他们面临的挑战，他们如何开始用 AWS 服务解决这些问题，特别是 Amazon SageMaker。

![](img/624e3063a76c2dc1232731d5cc10f772.png)

Tell me about your first GPU cluster.

信不信由你，我保证你在下面读到的一切都是 100%基于无数的客户互动。

# 爱丽丝医生

爱丽丝拥有博士学位，在一家大型公共研究实验室工作。她是一名训练有素的数据科学家，在数学和统计学方面有很强的背景。

她把时间花在大型科学项目上(生命科学、物理学等)。)，涉及庞大的数据集(几 TB，往往更多)。她可以用像 Matlab、R 和 Python 这样的高级语言编写数据分析代码:也许它看起来不怎么样，但确实有用。

Alice 通常不太了解 IT 和基础设施，老实说，她根本不关心这些话题。她的重点是推进她的研究，发表论文，等等:其他一切都是“工具”。

对于日常工作，她可以依靠自己强大(但昂贵)的桌面工作站:高端英特尔 CPU、64GB 内存、4TB 本地存储和几个中端英伟达 GPU。她认为自己很幸运有一个这样的人(并不是她的所有同事都这样)，她很高兴自己可以独自工作“*”。不过，如果她想保持合理的训练时间，她只能用一小部分数据集进行实验。*

她每天晚上和每个周末都运行长时间的工作负载，希望它们不会崩溃…或者没有人会关掉她办公室的电源。当这种情况发生时，她叹了口气，然后重新开始工作。“浪费时间和精力又有什么用呢？”她想，但她对此无能为力。

她试图自己维护她的机器的软件配置，因为它不太了解她使用的深奥工具。尽管如此，她还是希望有人能为她这么做:NVIDIA 驱动程序、Tensorflow 依赖项等等让人感到相当困惑。当出现问题时，她会浪费宝贵的时间来修理“ *IT 设备*，这令人沮丧。当爱丽丝想要运行大型实验时，她必须使用托管在计算中心的远程服务器:一群非常强大的多 GPU 服务器，连接到 1pb 的 NAS 存储。当然，她必须与其他研究人员共享这些服务器。每周，团队领导都要会面并尝试对项目和工作量进行优先排序:这从来都不容易，决策往往需要上报给实验室主管。宝贵的时间被浪费了，有时实验无法在会议提交截止日期前完成。主管承诺明年的预算将考虑更多的服务器，但即使它们获得批准，采购和部署它们也需要几个月的时间。为了帮助安排工作量，Alice 雇佣了一名暑期实习生来编写一个简单的内部网门户，研究人员可以在那里手动预订服务器。它有点工作，但有时她的同事忘记发布服务器…或者他们不愿意发布服务器，因为他们知道他们必须等待获得另一个服务器。爱丽丝认为一定有更好的方法，但解决这个问题不是她的工作。不管怎样，她尽量用她能得到的东西来凑合。她不禁想到，如果她的实验不受容量限制，她会取得更大的进步。

最后但并非最不重要的一点是，Alice 受邀与位于另一个大陆的世界级实验室合作。在过去的一个月里，她一直试图找出如何与他们共享数据和基础设施。连接是复杂的，鉴于数据集的规模，数据传输几乎是不可能的。再次，“ *IT 材料*”阻碍了她的研究，她开始认为必须有一种更快更简单的方法来完成所有这些…也许云计算的东西可以有所帮助？

# 塞格马克土地上的爱丽丝医生

经过一些个人研究和数周的内部讨论，Alice 已经说服实验室主任让她试验 AWS，特别是那个看起来很有趣的 Amazon SageMaker 服务。

在短短几个小时内，她阅读了在线文档，快速创建了一个便宜的[笔记本实例](https://docs.aws.amazon.com/sagemaker/latest/dg/nbi.html)，并开始运行一些[样本笔记本](https://github.com/awslabs/amazon-sagemaker-examples)，以熟悉这项服务及其典型的工作流程。尽管她对 AWS 或 Python 了解不多，但她相信 [SageMaker SDK](https://github.com/aws/sagemaker-python-sdk) 正是她所需要的，她很快就会上手。她甚至找到了一个关于如何为她心爱的 R 语言[创建定制环境的样本笔记本！

在 IT 的一点帮助下，爱丽丝上传了几兆字节的真实生活数据到](https://github.com/awslabs/amazon-sagemaker-examples/tree/master/advanced_functionality/r_bring_your_own)[亚马逊 S3](https://aws.amazon.com/s3/) ，以便在亚马逊 SageMaker 上复制她的桌面环境。在更多的阅读之后，她了解到只需要几行代码就可以[在托管实例上训练她的模型](https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-training.html)，并且她将只为她实际使用的东西付费。她甚至可以根据需要在任意多的 [*p3.16xlarge*](https://aws.amazon.com/ec2/instance-types/p3/) 实例上训练她的模型:每一个都配备了八个 NVIDIA V100 GPUs！这与计算中心的大型服务器的配置相同。她现在可以按需创建它们:不再与其他团队争论。

得益于分布式训练和[管道模式](https://aws.amazon.com/blogs/machine-learning/accelerate-model-training-using-faster-pipe-mode-on-amazon-sagemaker/)等高级功能，Alice 发现在自己的大型数据集上训练模型很容易:一切都开箱即用，伸缩自如。Alice 也很高兴看到 SageMaker 包含了一个[自动模型调整](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning.html)模块:由于这个，她能够在仅仅几个小时的并行优化中显著提高她的模型的准确性。由于缺乏计算资源，用她以前的设置做这些是不可能的。

[部署模型](https://docs.aws.amazon.com/sagemaker/latest/dg/deploy-model.html)很简单:Alice 可以选择将模型部署到实时端点，或者运行批量预测。后者对她最有用，因为她需要偶尔预测大量数据。同样，只需要几行代码:她实际上复制粘贴了样本笔记本中的所有内容。最后但并非最不重要的一点是，跟踪她的支出很容易:AWS 控制台会告诉她花了多少钱，爱丽丝还可以设置预算警报。在与 IT 部门的同事交谈时，Alice 意识到 AWS 还有很多功能。看起来实验室可以使用名为 [AWS Snowball](https://aws.amazon.com/snowball) 的服务轻松上传数百兆字节到亚马逊 S3！与已经是 AWS 客户的其他实验室和大学共享这些数据看起来并不复杂。爱丽丝期待着合作和创新的步伐加快！

短短一周左右，她对它的整个看法都变了。她说:“*这个云东西实际上非常酷*”。过去，AWS 阻碍了我的发展，但现在，它确实帮助我提供了比以前更好、更快、更便宜的结果。

# 云原生 Bob

鲍勃在一家大公司工作。他是一名后端软件工程师，从记事起就一直与数据打交道:SQL、NoSQL、Hadoop、Spark 以及现在的机器学习。使用现成的库(主要是 scikit-learn，还有一点 Tensorflow)，Bob 和他的队友处理企业数据来训练数百个 ML 模型:线性回归、分类、分段等。繁重的工作(ETL、清理、特性工程)正在运行一个大的 Spark 集群。Bob 的公司使用 AWS 已经五年多了。所有开发、QA 和生产基础设施都托管在那里，他们是 DevOps 和云原生技术的忠实粉丝。最初，他们把一切都建立在[亚马逊 EC2](https://aws.amazon.com/ec2/) 上，因为他们觉得拥有完全控制权很重要。两年前，他们将 Spark 集群迁移到了[亚马逊 EMR](https://aws.amazon.com/emr/) ，还决定使用 Docker containers 实现标准化生产:他们现在 100%的工作负载都部署到了一个大型的[亚马逊 EKS](https://aws.amazon.com/eks/) 集群，因为 Kubernetes 是如此之酷，也因为从笔记本电脑到生产的无缝开发体验。他们根据建立了所有的 CI/CD 工具链，并使用 Terraform 实现了一切自动化。使用[自动缩放](https://aws.amazon.com/ec2/autoscaling/)和[点实例](https://aws.amazon.com/ec2/spot/)优化成本。这些人真的很了解他们的东西，他们被邀请在下一次 AWS 峰会上展示他们的架构。当然了。

当然，他们的 ML 工作负载也运行在 EKS 集群上(大部分是在 CPU 实例上，也有一些 GPU)。Bob 为训练和预测维护定制的容器:库、依赖项等。这需要一点时间，但他喜欢这样做。他只是希望没有人会要求他也做 Pytorch 和 Apache MXNet。Bob 听说过[深度学习 AMI](https://aws.amazon.com/machine-learning/amis/) 和[深度学习容器](https://aws.amazon.com/machine-learning/containers/)。检查那些东西在他的任务清单上，但是他现在没有时间。

最初，Bob 希望让每个数据科学家使用 Terraform 模板创建他们自己的按需集群，但他担心成本难以管理。此外，创建一个集群需要 15-20 分钟，团队肯定会抱怨这一点。相反，Bob 建立了一个大型的共享培训集群:用户可以在几秒钟内开始他们的分布式工作，Bob 管理单个集群更简单。已经设置了自动扩展，但是仍然需要容量规划来找到预留、现场和按需实例的正确组合。

Bob 每周与团队开会，以确保他们有足够的实例…当他们需要额外的容量时，他们还会让他随时待命。Bob 尝试在晚上和周末集群不太忙的时候自动减少容量，但他很确定他们的花费太多了。哦好吧。

一旦模型经过训练和验证，Bob 会将它们推送到 CI/CD，它们会自动部署到生产集群。绿/蓝部署、服务发现、自动扩展、将日志推送到[弹性搜索](https://aws.amazon.com/elasticsearch-service/)集群等。:整个九码。Bob 对他构建到系统中的自动化水平感到非常自豪，这是理所当然的。

# 云土著鲍勃在 SageMaker 土地

鲍勃已经在 SageMaker 上观看了一个 [AWS 视频](https://www.youtube.com/watch?v=ym7NEYEx9x4)。他喜欢基于 Docker 的训练和预测，并且内置框架的容器是开源的:那么就不需要维护他自己的容器了。

将培训工作负载迁移到 SageMaker 看起来很容易:Bob 可以摆脱 EKS 培训集群，让每个数据科学家完全按需进行培训。随着 Spot 实例[即将推出](https://aws.amazon.com/blogs/aws/aws-new-york-summit-2019-summary-of-launches-announcements/)，Bob 当然可以进一步优化培训成本。

就预测而言，Bob 会考虑将批处理作业转移到 SageMaker，但不会转移实时 API:根据公司政策，这些必须部署到 EKS。这不成问题，因为他可以重复使用相同的容器。

几个星期后，鲍勃实现了所有这些改变。数据科学团队现在从实验到培训都是完全自主的，这是他们喜欢的:容量不再是问题，每周会议也变得没有必要。此外，由于 SageMaker 提供了已训练模型的可追溯历史，Bob 也发现自动化模型再训练和重新部署更容易:以前，他必须让数据科学团队来做，这个过程对他来说太不确定了。

像分布式训练、管道模式和自动模型调整这样的高级功能也相当不错。数据科学团队很快就采用了它们，这为他们节省了大量时间。此外，他们不再需要维护自己编写的代码来实现类似的东西。只有一个问题:现在，Bob 必须更新他的 AWS 峰会幻灯片，以说明 SageMaker 用例。也许当地的福音传道者可以帮助他？；)

一如既往的感谢您的阅读。很乐意在这里或者在 [Twitter](https://twitter.com/julsimon/) 上回答问题(DMs 开放)。也可以随意分享你自己的趣闻轶事！

*我举起我的号角，向世界各地的人们致敬。继续建，我的 M(eta)L 兄弟姐妹:)*