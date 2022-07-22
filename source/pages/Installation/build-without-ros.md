# 通过源码编译 SDK

```{toctree}
:maxdepth: 1
:glob:
```


```{contents} 目录
:depth: 2
:local:
```

您可以选择在不依赖 `Ros` 的情况下对 SDK进行编译。但 `SDK` 依然是通过串口进行工作的，请确保您有可识别的串口设备。

## 编译静态链接库

```bash
git clone https://github.com/DDTRobot/diablo-sdk-v1.git
cd diablo-sdk-v1
vi CMakeLists.txt

#将 WITH_ROS 设为0
set(WITH_ROS  0)

mkdir build && cd build
cmake .. 
make 
```

编译完成后，您将会获得 `libdiablo_sdk.a` 的静态链接库。


