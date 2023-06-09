# 气流 KubernetesExecutor

> 原文：<https://towardsdatascience.com/kubernetesexecutor-for-airflow-e2155e0f909c?source=collection_archive---------2----------------------->

## 在 Kubernetes 上自然缩放气流

在 1.10 版本中，Airflow 引入了一个新的执行器来大规模运行 workers:Kubernetes 执行器。在本文中，我们将探讨:

*   什么是气流，它解决什么问题
*   库伯内特遗嘱执行人及其与芹菜遗嘱执行人的比较
*   minikube 上的示例部署

# TL；速度三角形定位法(dead reckoning)

气流有了一个新的执行者，可以在 Kubernetes 上自然产生工蜂。在这个 [git 库](https://github.com/BrechtDeVlieger/airflow-kube-helm)中有一个导航图，以及一些帮助你开始使用 KubernetesExecutor 的例子。

# 气流作为工作流调度程序

![](img/fc65b27c284e4195d157b772879398bf.png)

[Background image](https://unsplash.com/photos/nZL80Di-YAg)

数据工程领域迅速发展，以处理和存储不断增长的数据量。现在有很多技术可以在所谓的数据湖或数据仓库中存储和查询数 Pb 的原始数据。想想开源平台——Hadoop、Kafka、Druid、Ceph——或者云原生解决方案——亚马逊红移和 S3、谷歌 BigQuery 和 GCS、Azure 数据仓库和数据湖。你可以使用 Spark、Flink、Storm 或 Beam 等工具来处理这些海量数据。或者在数据仓库上运行查询，并将结果存储在新表中。数据管道通常由许多步骤和工具组成，用于移动数据。那么，我们如何将这些组件缝合到一个可靠的工作流中呢？

工作流调度程序管理任务之间的依赖关系，并协调它们的执行。知名的调度有[气流](https://airflow.apache.org/)、[路易吉](https://luigi.readthedocs.io)、 [Oozie](http://oozie.apache.org/) 和[阿兹卡班](https://azkaban.github.io/)。Airflow 因其丰富的 UI、灵活的配置和编写定制扩展的能力而获得了社区的大力支持。Airbnb 启动了这个项目，并将其开源为 Apache 孵化器。

想象一下，我们有一堆数据放在谷歌云存储(GCS)的某个地方，等待处理。我们希望使用 Spark 清理数据，并将其移动到 BigQuery 进行分析。预算紧张，所以我们没有全天候运行的 Hadoop 集群。我们首先要创建一个新的 Dataproc 集群(Dataproc 是 Google Cloud 上的 Hadoop)。然后，Spark 作业从 GCS 获取数据，对其进行处理并将其转储回 GCS。最后，BigQuery 作业将数据从 GCS 加载到一个表中。同时，我们可以关闭 Dataproc 集群来清理我们的资源。这是这样一个气流工作流程的样子。

![](img/e2904f0ef2f8f7178a8ec582d9b4ff8d.png)

气流本身支持上述所有步骤以及更多。Airflow 还负责对 GCS、Dataproc 和 BigQuery 的认证。这是一个简单的示例，说明了气流如何在任务之间创建工作流。如果你是气流的新手，我强烈推荐你在 Github 上查看[这个资源管理。这篇文章假设你已经理解了气流的本质。](https://github.com/jghoman/awesome-apache-airflow)

# 规模化气流

![](img/6e4b125c70ac3008b9e6d73241cffa0f.png)

[Background image](https://unsplash.com/photos/ZpeCkOiiQUo)

气流不仅仅可以运行数据管道。它可以触发任何带有 API 的作业。这开启了一个充满机遇的世界！不知不觉中，你的气流装置变得挤满了管道。是时候扩大规模了。Kubernetes 是扩展应用的领先技术之一。应用程序的各个部分在所谓的 pod 中作为独立的容器运行。当应用程序需要更多功率时，Kubernetes 会复制这些 pod。

Airflow 的架构非常适合这种模式。在其核心，调度程序决定哪些任务需要运行下一步。web 服务器使用户能够与 Dag 和任务进行交互。数据库跟踪当前和过去作业的状态。最后，气流有运行任务的工人。调度程序、web 服务器和数据库通常不需要扩展。完成繁重任务的是工人节点。Airflow 有两个流行的执行器可以大规模部署工作人员 CeleryExecutor 和 KubernetesExecutor。

[Celery](http://www.celeryproject.org/) 是一个分布式任务队列，在多个节点之间平衡工作负载。使用芹菜在工人节点上调度作业是一种流行的扩展气流的方法。[在这里](https://github.com/mumoshu/kube-airflow)您可以找到一张导航图，使用 CeleryExecutor 自动完成部署。但是，如果使用芹菜效果如此之好，那么我们为什么还需要另一个 Kubernetes 的执行者呢？因为芹菜挺复杂的。您需要在系统中部署芹菜作为额外的组件。而芹菜需要 RabbitMQ 或 Redis 这样的经纪人作为后端。此外，您可能希望用 web 界面 Flower 来监控芹菜。也许这些组件对于手头的任务来说增加了太多的开销？我们不能来点更简单的吗？是啊！Airflow 1.10 引入了一个新的执行器来扩展工作人员:Kubernetes 执行器。

对于芹菜，你在前面部署几个工人。然后，队列将在它们之间调度任务。相比之下，KubernetesExecutor 不会持续运行任何工人。相反，它为每项工作产生了一个新的工人群体。工作完成后，气流会立即清理资源。现在我们充分利用 Kubernetes 的潜力。不再需要额外的组件。扩展仅受限于集群的大小。只要你有足够的 CPU 和内存可用，气流可以不断调度更多的任务。当 Airflow 不再有作业运行时，只有调度程序、web 服务器和数据库保持活动状态。您的群集可以将其资源用于其他应用程序。

# 实践中的 Kubernetes 执行者

让我们深入实际细节。这篇文章的剩余部分将通过一个简单的例子来说明。我们将使用[掌舵图](https://github.com/BrechtDeVlieger/airflow-kube-helm)在 minikube 上设置气流，但是如果你愿意，你可以在任何云提供商上部署它。我们的部署将定期从 Airflow 的 git 存储库中同步 Dag。让我们从克隆 git 存储库开始。

```
git clone [https://github.com/BrechtDeVlieger/airflow-kube-helm](https://github.com/BrechtDeVlieger/airflow-kube-helm)
cd airflow-kube-helm
```

在继续之前，请确保 minikube 已启动并正在运行。在 minikube 开始旋转仪表板后，您可能需要等待一分钟。

```
minikube start
minikube dashboard
```

首先，我们需要一个包含 Airflow 版本 1.10.2 或更高版本的 docker 映像。确保您已经安装了 Docker，并且 minikube 已经启动并正在运行。按照这些指南来安装和设置 docker 和 minikube。该存储库包含一个构建 docker 映像的脚本。

```
./examples/minikube/docker/build-docker.sh
```

该脚本使用 Kubernetes 依赖关系从 [docker-airflow](https://github.com/puckel/docker-airflow) 构建了一个新的图像。当脚本完成时，图像将在 minikube 的注册表中作为`airflow:latest`出现。

Helm charts 允许开发人员创建可重用的 Kubernetes 部署。Helm 读取 values.yaml 文件并生成一组 yaml 文件。这些文件描述了一个 Kubernetes 部署。我们只需创建一个新的 yaml 文件来覆盖默认设置，从而创建一个定制部署。你可以在这里找到所有的默认值及其解释[。我们将逐一介绍必要的更改。首先创建一个新的 values.yaml 文件。](https://github.com/BrechtDeVlieger/airflow-kube-helm/blob/master/airflow/values.yaml)

Airflow 使用 fernet 密钥对数据库中的密码进行加密。当然，我们不想以纯文本的形式存储它们。下面是生成这样一个密钥的方法。

```
python -c "from cryptography.fernet import Fernet; FERNET_KEY = Fernet.generate_key().decode(); print(FERNET_KEY)"
```

将生成的密钥粘贴到 values.yaml 文件中。

```
airflow:fernet_key: "j0PNE8131Vx-ix7BsNDwskFUlnLa00mWU17BRujVcdY="
```

接下来，我们必须告诉使用哪个图像。如果您在 minikube 上构建映像，那么配置如下所示:

```
airflow:
  ...
  image:
    repository: airflow
    tag: latest
    pull_policy: IfNotPresent
```

`pull_policy`在 minikube 上无关紧要，因为它使用其本地注册表来获取气流图像。

我们必须告诉气流从哪里得到这些数据，以及如何存储它们。我们的示例定期从[气流存储库](https://github.com/apache/airflow/tree/master/airflow/example_dags)获取示例 Dag，并将它们复制到 Dag 文件夹中。以下代码片段向您展示了如何做到这一点:

```
airflow:
  ...
  dags:
    persistence:
      enabled: false
    git:
      url: [https://github.com/apache/airflow](https://github.com/apache/airflow)
      branch: master
      subpath: airflow/example_dags
      wait: 60
```

要从 git 中提取 Dag，必须禁用持久性。在大多数情况下，dag 不存在于根 git 文件夹中。在我们的例子中，我们必须在子目录`./airflow/example_dags`中寻找它们。我们将把这个目录传递给`subpath`参数。其默认值为`dags`。您可以使用`wait`字段配置从 git 获取 Dag 的频率。

在继续部署之前，确保您的 values.yaml 文件看起来像下面的代码片段。

```
airflow:fernet_key: "j0PNE8131Vx-ix7BsNDwskFUlnLa00mWU17BRujVcdY="
  image:
    repository: airflow
    tag: latest
    pull_policy: IfNotPresent
  dags:
    persistence:
      enabled: false
    git:
      url: [https://github.com/apache/airflow](https://github.com/apache/airflow)
      branch: master
      subpath: airflow/example_dags
      wait: 60
```

教程的其余部分是小孩子的游戏。只需几个命令，我们就能让气流流动起来。但首先，我们需要在 minikube 上安装 Helm。顺便说一下，我们把运行在 Kubernetes Tiller 上的 Helm 部分称为。我们还将安装所需的舵依赖。

```
kubectl apply -f airflow/tiller.yaml
helm init --service-account tiller
helm dependency update
```

使用 Helm 生成 yaml 文件并部署 Airflow。

```
helm upgrade --install airflow airflow/ \
    --namespace airflow \
    --values values.yaml
```

几分钟之内，气流就会开始流动。如果需要一点时间，请不要担心。通常，web 服务器和调度程序会在 Postgres 数据库准备好之前尝试连接到它。在 pod 失败并重新启动之前，连接需要超时。为了加速这个过程，只要数据库准备好，就手动重新启动 web 服务器和调度程序窗格。

当所有的 pods 都准备好时，您可以使用这个命令将 web UI 转发到 [http://localhost:8080](http://localhost:8080) 。

```
kubectl port-forward --namespace airflow $(kubectl get pod --namespace airflow --selector="app=airflow-web,release=airflow" --output jsonpath='{.items[0].metadata.name}') 8080:8080
```

现在尝试通过取消暂停来运行`example_bash_operator`。DAG 现在应该运行两次。在 minikube 仪表板上观察气流如何启动新的 pod 并清理已完成的 pod。您可以在图形和树视图中查看日志。遗憾的是，您无法从任务实例面板查看日志。这仍然是 KubernetesExecutor 中的一个 bug。

# 结论

气流 1.10 引入了一个新的执行器来大规模运行气流:KubernetesExecutor。调度器直接与 Kubernetes 交互，在任务开始和结束时创建和删除 pods。因此，当 Airflow 空闲时，只有调度程序和 web 服务器在运行。这为集群中的其他应用程序释放了资源。气流现在能够在 Kubernetes 上自然扩展，而不需要芹菜等附加组件。部署更加简单明了。

然而，新的执行程序仍然很新，有时表现有点出乎意料。1.10.2 版本解决了大部分问题，所以我建议只使用这个版本或更高版本。不过还有一个棘手的问题。日志卷需要允许从所有 Airflow pods 进行读写访问。云提供商本身不支持读写多个卷，因此您必须自己提供解决方案。该存储库包含一个 NFS 服务器的示例。

尽管如此，executor 按照预期工作，并且足够稳定，可以投入生产。气流的开发团队做得很棒。太棒了。谢谢你坚持到最后，希望这篇帖子能对你接下来的部署有用。