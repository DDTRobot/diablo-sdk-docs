# 安装与部署ROS

```{toctree}
:maxdepth: 1
:glob:
```


```{contents} 目录
:depth: 2
:local:
```



## 树莓派安装 Ros-noetic

- [安装 Ubuntu mate](https://ubuntu-mate.org/download/arm64/jammy/)
- [树莓派配置硬串口](./installing-sdk-on-pi)
- [安装 Ros-noetic](http://wiki.ros.org/noetic/Installation/Ubuntu)

Ros 的安装可能受到网络的影响，会导致安装出现问题。


## 编译 Ros Package

1. 创建ros工程文件夹

```bash
#make sure you have build all dependence.
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace

#clone API source code
git clone https://github.com/DDTRobot/diablo-sdk-v1.git

cd ~/catkin_ws
catkin_make
```

向 `.bashrc` 添加以下指令，保证您可以通过局域网访问`ROS机器人` 的节点。

```bash
export ROS_IP=${机载树莓派IP}
export ROS_MASTER_URI=http://${ROS_IP}:11311
```

