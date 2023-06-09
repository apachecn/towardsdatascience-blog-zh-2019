# PyTorch 的 HDF5 数据集

> 原文：<https://towardsdatascience.com/hdf5-datasets-for-pytorch-631ff1d750f5?source=collection_archive---------3----------------------->

![](img/eee154724880ba8b7182ca95920d9393.png)

如果你从事计算机视觉领域的工作，你肯定听说过 HDF5。**分层数据格式** (HDF)第 5 版是一种流行的格式，用于存储和交换非结构化数据，如 raw 格式的**图像、视频或卷**，以用于各种研究或开发领域。它受到许多编程语言和 API 的支持，因此变得越来越流行。这也适用于为机器学习工作流程中的**存储数据。在这篇文章中，我介绍了一种在 PyTorch 中使用 HDF5 数据训练深度学习算法的可能方法(包括即用型代码)。**

# HDF5 文件格式

HDF5 文件由**两种主要类型的对象组成:**数据集和组。数据集是同构类型的多维数组，例如 8 位无符号整数或 32 位浮点数。另一方面，组是为保存数据集或其他组而设计的层次结构，构建了类似文件系统的数据集层次结构。此外，组和数据集可能会附加用户定义属性形式的元数据。

Python 使用 [**h5py** 包](https://pypi.org/project/h5py/)支持 HDF5 格式。该软件包封装了原生 HDF C API，并支持该格式的几乎全部功能，包括读写 HDF5 文件。

如果你需要在可视化编辑器中查看或编辑你的 HDF5 文件，可以下载官方 [**HDFView**](https://www.hdfgroup.org/downloads/hdfview/) **应用**。该应用程序支持以表格方式或图像方式查看不同格式的数据集。此外，它使您能够通过创建新的组和数据集以及重命名和移动现有的组和数据集来编辑文件。

# PyTorch 数据集

为了高效地将您的数据加载到 PyTorch，PyTorch 要求您编写自己的 **Dataset** 类(或者使用预定义的类)。这是通过从**torch . utils . data . Dataset**继承，覆盖**函数 __len__** (以便在数据集上调用 len()返回数据集的长度)和 **__getitem__** (启用索引)来实现的。

然后使用类**torch . utils . data . data loader**以预定义的方式从数据集中进行**采样(例如，您可以随机打乱数据集，选择批量大小等)。PyTorch 中数据加载的主要优势(和魔力)在于这样一个事实，即**数据加载可以以并行方式**发生，而无需处理多线程和同步机制。这可以通过简单地将 DataLoader 构造函数中的参数 *num_workers* 设置为所需的线程数量来实现。作为在 PyTorch 中使用 Dataset 和 DataLoader 类的示例，请看下面的代码片段，它展示了如何在您的程序中使用 HDF5 数据集。我们将在下一节中研究如何实际实现数据集。**

# HDF5 数据集类

我设计 HDF5 数据集类时考虑了多个目标:

1.  使用包含 HDF5 文件的文件夹(包括子文件夹)作为数据源，
2.  在数据集中维护一个简单的 HDF5 组层次结构，
3.  启用惰性数据加载(即应数据加载器的请求)为了允许处理不适合存储器的数据集，
4.  维护数据缓存以加快数据加载过程，以及
5.  允许数据的自定义转换。

我决定在数据集上实施一个简单的结构，该结构由放置在不同组中的各个数据集组成，如下所示:

![](img/9f94bdc2518b28fd95b7978f63248bdb.png)

这反映了许多机器学习任务的通常数据结构。通常，每个组中都有一个包含数据的数据集，以及一个或多个包含标签的数据集。例如，用于图像分割的数据集可能包括要分割的图像(一个数据集)以及地面实况分割(另一个数据集)。这些标签被放在一个组中，以便确定哪些标签属于哪些数据。此外，可以通过将不同类型的数据放置在不同的 HDF5 文件中来构建更高级别的语义层次(例如，由不同用户执行的分段)。

事不宜迟，下面是实际代码:

如您所见，数据集通过搜索目录(和子目录)中的所有 HDF5 文件进行初始化，并构建一个 data_info 结构，其中包含有关每个数据块的信息，例如它来自哪个文件、它的类型(在本例中为“数据”或“标签”，但您可以定义其他文件)及其形状。形状通常有助于确定数据集的大小，因此它是需要存储的重要信息。此外，对于每个块，我们还存储其数据缓存索引。如果数据当前已加载，则索引≥0，如果尚未加载，则索引为-1。

如果数据加载器现在请求一些数据，则调用 *__getitem__* 函数，该函数又调用 *get_data* 函数。注意，在这里我们不能只索引某个数组，因为我们首先必须确保数据确实在内存中。因此，在 *get_data* 中，我们查找缓存以找到数据，或者，如果数据不在缓存中，我们加载它并将其返回给调用者。这发生在 _load_data 函数中，该函数做两件事:加载数据并将其添加到缓存中，如果超过了 *data_cache_size* ，则从缓存中移除随机的数据块。

获得数据后，必须根据您在构造函数中提供的转换对其进行转换，并将其转换为 torch。张量类型。

# 结论

在这篇文章中，我展示了一个简单但功能强大的 HDF5 数据集类，您可以使用它在 PyTorch 中加载 HDF5 数据集。我希望它对你有用。如果您有任何问题或进一步的建议，请不要犹豫，在下面留言。