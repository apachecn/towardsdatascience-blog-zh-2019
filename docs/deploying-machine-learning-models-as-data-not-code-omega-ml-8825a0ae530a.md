# 将机器学习模型部署为数据，而不是代码——更好的匹配？使用 omega|ml 的 MLOps

> 原文：<https://towardsdatascience.com/deploying-machine-learning-models-as-data-not-code-omega-ml-8825a0ae530a?source=collection_archive---------20----------------------->

*数据科学界的使命是找到部署机器学习解决方案的最佳方法。我的 MLOps 开源框架 omega|ml 通过将模型部署为数据来实现一种新颖的方法，提高了速度和灵活性，同时降低了工具链的复杂性。*

![](img/711fb2e1795611b65447890a6e7f4edc.png)

Photo by [Stephen Dawson](https://unsplash.com/@srd844?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/artificial-intelligence?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

**用于机器学习的 DevOps:不完全匹配**

当涉及到部署机器学习模型时，mlflow 和 kubeflow 等工具促进了 DevOps 原则的使用，即像代码一样打包模型，将它们作为软件发布的一部分进行部署。乍一看，这种方法提供了几个期望的属性:

*   模型和其他代码一起被版本化
*   模型发布是作为一个单元构建、打包和部署的
*   部署是可重复的，回退是可能的

然而，当我们将这种 DevOps 方法应用于机器学习时，我们的部署缺少运行有效的机器学习解决方案所需的其他关键属性。

特别是，在任何协作环境中，更重要的是在多产 ML 系统中，我们希望:

*   立即共享和部署新模型
*   在生产中自动重新训练模型
*   捕获运行时模型输入，供以后在质量保证中使用
*   运行多个模型版本(rendezvous 架构)

**关键观察:模型本质上是数据**

> 机器学习模型本质上由给定的算法+权重+超参数组成。权重和参数是数据，而不是代码，而任何特定模型的算法都是对静态库的引用。从这个角度来看，将模型视为数据比围绕权重+超参数创建包装语义更自然。

实现这一点的一种方法是构建额外的工具和基础设施，在更传统的 DevOps CI/CD 流程之上获得这些属性。然而，我建议重新思考这个问题，将模型视为数据，而不是代码。

**使用 omega|ml，将模型作为数据进行部署是非常简单的**

将模型视为数据而非代码是什么意思？在 omega|ml 中，可以直接从 Python 代码中部署模型:

```
clf = LogisticRegression() # scikit learn model
om.models.put(clf, 'mymodel') # store the model
```

这将模型`clf`存储为 joblib-pickle 文件，并在 omega|ml 的内置分析存储中创建一个`Metadata`条目。它还在`/api/v1/model/mymodel`创建了一个 REST API 端点，以便可以从任何应用程序、任何编程语言访问该模型。部署是即时的，没有延迟，不需要打包或 CI 过程，也没有任何显式的部署步骤:不需要构建、部署和启动容器。

**在集群中本地或远程安装模型**

*“等待”*，你说，*“我们还没有拟合模型，那么部署模型有什么用？”*。omega|ml 可以部署未安装和安装的型号。如果模型不合适，我们可以远程训练模型，即使用 omega|ml 的计算集群:

```
om.runtime.model('mymodel').fit(X, Y)
```

这将选择一个计算节点，将 X 和 Y 数据加载到内存中，并运行`clf.fit(X, Y)`方法。完成后，它将以相同的名称存储现在适合的模型，有效地用适合的版本替换先前不适合的模型。我们可以随时在集群中重新运行`fit`方法。也可以运行任何其他建模方法，如`partial_fit, score, gridsearch`等。

传递给`fit`方法的`X,Y`参数或者是内存中的数据对象(如 Pandas DataFrames、Series 或 Numpy ndarrays)，或者是之前保存的命名对象，例如:

```
# save data, a pd.DataFrame
om.datasets.put(data, 'mydata')# assuming data has several feature columns with a target variable om.runtime.model('mymodel').fit('mydata[^Y]', 'mydata[Y]')
```

**开发与生产分离**

分离开发和生产在任何软件系统中是重要的，这些软件系统在被有效使用的同时经历了积极的开发。机器学习系统也是如此。omega|ml 通过*对象提升的概念支持环境分离:*

```
# om_prod is the production instance
om.models.promote('mymodel', om_prod.models)
```

生产实例可以是 omega|ml 在生产集群中的单独部署，也可以利用内置的 *bucket* 功能:

```
# here the production-bucket is a logical namespace 
om_prod = om['production-bucket']
```

**它是如何工作的？**

omega|ml 的任何实例都提供并运行数据科学团队所需的所有组件，无论是在开发中还是在生产中:

*   **多用户 Jupyter 笔记本:**数据科学家可以在共享的 Jupyter 主机上工作，或者在用户特定的实例上工作。笔记本可以通过一个简单的命令和类似人类的时间表轻松安排，例如*“每天早上 6 点”。*
*   **分析商店:**内置的分析商店提供结构化和非结构化存储(由 MongoDB 支持)，包括可扩展的分布式文件系统。使用 omega|ml 的插件机制可以添加任何存储后端。内置的分析存储意味着团队可以立即高效地开始工作，而无需从/向其笔记本电脑或从/向一些外部托管的对象存储进行耗时且低效的文件复制。这也意味着公司可以重新集中安全地组织用于机器学习的数据，降低由于无意中复制到潜在不安全的位置(如笔记本电脑的硬盘)而导致数据泄露的风险。
*   **计算集群:**虽然今天的台式机和笔记本电脑甚至有足够的资源用于机器学习，但利用云在许多情况下是有用的，如果不是必要的话。例如，数据集处理和模型训练可以异步、整夜运行，或者使用仅由云提供商提供的 GPU 运行，而无需持续连接或保持本地工作站运行。omega|ml 专为云设计，内置了强大的可扩展运行时架构。它支持训练模型和有效处理大型核外数据集，连接 GPU 或其他资源是一个配置问题。

此外，omega|ml 提供了各种 API 来满足不同的需求。

*   **模型、数据集和 lambda 风格/无服务器脚本的 REST API** (部署和运行任意 Python 模块)
*   **可扩展的 Python API** 利用 Flask、Django 或 Plotly Dash 等构建后端应用和 web 应用。
*   **命令行客户端(cli)** 支持任何开发和脚本环境。cli 还支持使用本地 ide，如 Pycharm 或 Jupyter Notebook 的本地实例，并将笔记本和自动构建的 PIP 包部署到 omega|ml 运行时。

> 请注意，对于 omega|ml 支持的任何模型，部署方式都是相同的，例如任何 scikit-learn 模型(包括管道)、Tensorflow 和 Keras 模型。此外，omega|ml 提供了一种易于扩展的插件机制，以完全相同的方式支持任何其他机器学习框架。

**一种方法，多种好处**

将模型部署为数据意味着数据科学团队可以同时完成几件事情:

*   **协作**:一旦模型被保存到数据存储中，其他团队成员可以很容易地检索模型，并在本地或远程使用它:

```
# retrieve the model locally 
clf = om.models.get('mymodel')
=> clf is the last saved LogisticModel# score the model remotely, using some new in-memory data in X, Y
om.runtime.model('mymodel').score(X, Y)# run a gridsearch remotely, saving the best model
om.runtime.model('mymodel').gridsearch(X, Y, parameters=...)
```

*   **生产中重新训练:**由于模型作为对象存储在数据库中，生产中的重新训练和部署就像运行一个作业一样简单，该作业在模型上重新运行`fit`方法:

```
# assuming the new data is in saved objects newX, newY
om.runtime.model('mymodel').fit('newX', 'newY')
```

*   **捕获用于预测的数据:**通过 REST API 传递到模型中的任何数据都会在预测之前自动保存(这个特性还有改进的空间，相应的插件正在开发中)。或者，我们可以通过 REST API 或 Python API 存储预测后的数据

```
# store the input and output data after prediction from Python
om.datasets.put(inout, 'predicted-upondata')
# use the REST API
PUT /api/v1/datasets/predicted-upondata/ (+ JSON body
```

*   **run-multiple model versions**:将模型视为代码，使用一个命名约定来部署多个模型版本是很容易的，然后并行运行模型，并通过一些聚集来选择最佳结果。

```
# store
om.models.put(model1, 'mymodel-1')
om.models.put(model2, 'mymodel-2') # run in parallel, note each call is asynchronous
y1 = om.runtime.model('mymodel-1').predict(X)
y2 = om.runtime.model('mymodel-2').predict(X)# aggregate y1 or y2 in some way once results are available
...
```

请注意，这只是 omega|ml 支持多模型版本的一种方式，其他方式包括虚拟对象处理程序(将多个模型组合在同一名称下)或使用脚本/lambda 模块(使用`om.runtime.job('script-name').run())`运行任意代码)

**结论**

当将模型视为代码时，使用 DevOps 原则部署模型是一个显而易见的选择。然而，它在几个期望的属性上有所欠缺，如即时部署、协作、生产中再培训、用于质量保证的运行时数据收集以及以 rendevouz 风格运行多个模型版本。因此，将 DevOps 方法应用于机器学习——实际上是数据科学——需要额外的投资和工具来实现这些特性。

omega|ml 认为模型是数据，而不是代码。这实现了从实验室到生产的开发和操作数据科学和机器学习系统的所有期望属性。也就是说，omega|ml 帮助数据科学团队高效利用云资源，在机器学习模型和数据上进行合作，并轻松实施他们的 ml 解决方案。事实上，使用 omega|ml，部署机器学习模型只需一行代码。

更多信息请访问 [http://get.omegaml.io](http://get.omegaml.io)