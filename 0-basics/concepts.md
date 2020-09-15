# Amazon SageMaker 概念

## 概览

SageMaker 是 AWS 的机器学习托管服务，主要提供 Jupyter Notebook 和虚拟机（下称「实例」）的托管。

## 组件

SageMaker 由如下组件组成：

- **Notebook 实例托管**。SageMaker 帮助用户创建、管理用于运行 Jupyter Notebook 的实例。
- **任务管理器**。用户将数据预处理、训练和推理的应用打包成容器镜像，由 SageMaker 负责执行。
  - **训练任务**。托管的训练任务有如下好处：实例初始化和镜像、输入下载都不收费，开始训练才收费；支持使用竞价实例（折扣率 30-90%）；在训练效果没有提升时提早结束训练。
  - **超参数调优任务**。用户为超参数设置调优范围，由 SageMaker 在范围内使用不同超参数进行训练，找出最优组合。
- **内置算法**。即预先制作好的训练/推理算法容器镜像，覆盖多个常见场景，用户可以直接使用。
- **节点管理器**。用户设置想要部署的节点实例类型和数量，由 SageMaker 负责部署模型到节点，用于推理。
- **SageMaker Studio**。托管的修改版 Jupyter Lab，对接 Amazon EFS 存储（类似网盘），支持多人协作，预装了 SageMaker 相关的多个插件。
- **SageMaker Autopilot**。针对特定类型的输入、输出数据集（CSV），自动尝试多种不同算法和参数，找到对应关系最好的一种。
- **SageMaker Debugger**。自动捕捉在训练过程中容易遇到的错误，比如初始参数导致设置有误导致的梯度爆炸（Exploding Gradients），输出错误信息并提前结束训练。
- **SageMaker Experiments**。用户在训练、优化和探索的时候经常会尝试不同的输入、输出、参数、配置，管理不便，所以 SageMaker 提供一个管理界面来管理这些尝试，是 SageMaker Studios 的内置功能。

## SDK

在 AWS 的服务中 SageMaker 的 SDK 算比较多的，容易混淆。它主要有如下几个 SDK：

- **AWS SDK**。即底层 SDK，属于 AWS 官方 SDK 的一部分，支持多种语言，但是基本上没有封装。此 SDK 与 AWS 的 REST API 有高度对应关系，参数也用类似 JSON 的对象来传输，使用不便（比如参数类型和格式错误可能无法提前捕捉）。
- **SageMaker Python SDK**。SageMaker 官方推出的基于 Python 的 SDK，对底层 API 进行了封装，所有的参数都以变量方式传入，更方便。由于底层 API 被拆成了 `Estimator`、`Predictor`、`Model` 等概念，所以有一定的学习成本。少量底层 API 的功能还没封装完善。目前已经发展到了 `v2` 版本，与第一版有多处不兼容。
- **SageMaker Experiments SDK**。SageMaker Experiments 是内置在 SageMaker Studios 里面的功能，但是目前在 Studios 里面没有提供创建和编辑试验的图形界面，需要使用这个 SDK 来进行试验的创建。






