# 创建 Notebook 实例

SageMaker 提供的一个基本功能就是托管的 Jupyter Notebook 实例。说白了其实就是预装了 SageMaker 的 EC2 实例。

与 EC2 实例相同，Notebook 实例也使用 IAM 角色，并在本地存储数据。创建时我们需要选择存储的大小，并且选择或者创建 IAM 角色（其实就是 EC2 上的实例配置文件）。

### 前后端分离

Notebook 实例有两种用法。一种是直接在 Notebook 内做训练，一种是只把 Notebook 当做是一个前端界面，把实际的训练扔给 SageMaker 来运行。

在本地训练时我们一般使用前一种方式，因为机器已经买了，一直开着也无所谓。在云端训练我们通常使用后一种方式，因为在前端界面展示时我们只需要最小的机器，只在训练的时候开启昂贵的机器用于训练。

### 无状态化

在云端通常建议做到存算分离，即存数据的服务的只管存数据，计算的服务只管计算。其结果，就是计算服务通常不保存状态，除了临时状态外大部分的状态和数据都放在存储服务中。这使得计算和存储可以各自进行扩容和缩容。

在计算服务上，存算分离的具体体现就是计算服务呈现「无状态化」。

```
就 SageMaker 托管的 Notebook 实例来说，无状态化的体现，就是其内置的库在每次重启之后都会重置。这一点需要尤其注意，因为它和本地机器的逻辑，甚至和 EC2 自建 Notebook 的逻辑都不同。

我们不能只对本地的库进行一次修改或者升级，然后期待它在重启之后还可以保留这些升级。在重启之后，SageMaker 会把内置的环境刷新，我们的修改就会失效。要想保留修改，就应该在 Notebook 中明确这些修改，这样每次执行 Notebook 时都会执行这些修改，重启也没关系。
```

我们自己安装

#TODO 文档错误

https://docs.amazonaws.cn/en_us/sagemaker/latest/dg/ecr-cn-northwest-1.html#xgboost-cn-northwest-1.title

amazonaws.com 写错了

### 内置库

SageMaker 的 Notebook 实例内置了一些库：

- scikit
- Pandas
- NumPy
- TensorFlow
- MXNet

### 本地 Notebook

我们也可以不使用 SageMaker 托管，而在本地运行笔记本实例，只把 SageMaker 当做是一个 SaaS 化的机器学习训练服务。这需要我们使用内置的算法，或者把自己的算法按照 SageMaker 的标准保存成容器镜像。

## 使用

### 上传 Notebook 文件

直接在 Notebook 界面选择「Upload」则可以上传在本地做好的 `.ipynb` 文件。