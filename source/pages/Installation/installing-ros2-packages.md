# 安装与部署ROS2

```{toctree}
:maxdepth: 1
:glob:
```


```{contents} 目录
:depth: 2
:local:
```



## X3 Pi 安装 DIABLO_ROS2

- [安装旭日X3派系统镜像](https://developer.horizon.ai/resource)
- [地平线机器人平台](https://developer.horizon.ai/api/v1/fileData/TogetherROS/index.html)

```{tip}
如果您安装了 foxy 的软件包，而编译的过程中识别不到。这可能是软连接的问题，可以尝试 ``source /opt/ros/foxy/setup.bash`` 解决问题。由于地平线的更新比较频繁，一切与硬件平台相关操作以地平线官方文档为主。
```


## Raspberry Pi 安装 DIABLO_ROS2

- [Ubuntu-mate](https://ubuntu-mate.org/download/arm64/jammy/)
- [树莓派配置硬串口](./installing-sdk-on-pi)
- [安装Ros-foxy](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html)

```{warning}
Ros 的安装可能受到网络的影响，会导致安装出现问题。
```



## 编译 Ros Package

1. 创建ros工程文件夹

```bash
#make sure you have build all dependence.

sudo apt install python3-colcon-common-extensions
mkdir -p ~/diablo_ws/src
cd ~/diablo_ws/src

#clone API source code
git clone -b basic https://github.com/DDTRobot/diablo_ros2.git

cd ~/diablo_ws
colcon build
source install/setup.bash

#before starting the node , please check of serial port in diablo_ctrl.cpp is correct.
ros2 run diablo_ctrl diablo_ctrl_node

#run controller python script
ros2 run diablo_teleop teleop_node 
```

向 `.bashrc` 添加以下指令，保证您可以通过局域网访问`ROS机器人` 的节点。

```bash
export ROS_DOMAIN_ID=5 
```

