> # 欢迎使用 DIABLO-Onboard-SDK 开发文档!
>

```{toctree}
:maxdepth: 3
:caption: DIABLO-Onboard-SDK 开发文档
pages/Installation
pages/How-to-Guides
pages/User-Example
pages/Related-Projects
```

## 简介

DIABLO OSDK是DIABLO双足轮式机器人系统配套的程序包,运行在机器人的机载小型电脑上。该程序包使用户可以在机器人上运行自定义程序，以验证用户自己开发的程序算法，实现用户所需的功能和应用，例如新型控制算法实践，自主智能导航和规划等功能。 DIABLO OSDK主要具有以下特点

* 兼容性优秀：软件设计上对环境依赖少，兼容多种硬件和用户使用的第三方程序包。

* 控制界面简单：用户可以通过我们提供的API，简单直观的向和机器人交互，收发指令。

* 安全性好：系统配套了多种安全保障逻辑，可以在用户开发过程中各种特殊工况下，尽可能保证安全。

您可以在我们的官网获得更多的产品信息 [本末科技](https://directdrive.com)。


### 如何开始

我们提供了机器人的控制结构，帮助您快速与自己的应用进行结合。您可以通过以[Ros](./pages/Installation/Build-Dependencies.md)节点的方式进行通信交互，也可以不依赖Ros直接对[SDK](./pages/Installation/Installing-SDK-On-Ubuntu.md)进行编译，依托于串口通信直接发送控制指令。

### 开发指南

您可以在[这里](./pages/User-Example.md)找到一些API的详细解释说明。

### SDK开发案例

您可以在[这里](./pages/User-Example.md)找到我们提供的一些使用案例，能够快速的帮助您连接机器人，测试自己的应用。

### 相关项目

您可以在[这里](./pages/Related-Projects.md)找到使用本末科技的直驱电机为基础构建的项目。



```{note}
  我们将致力于为您提供更多优质的机器人控制服务，依托于我们的机器人平台适配更多的智能算法，供您参考和学习，希望这能对您的研发工作有所帮助。

```
