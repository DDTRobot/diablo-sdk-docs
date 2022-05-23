# 在Ubuntu上部署ROS Noetic

```{toctree}
:maxdepth: 1
:glob:
```

```{contents} 目录
:depth: 2
:local:
```

本页介绍如何在Ubuntu Linux系统中构建 ROS Noetic。

```{note}
ROS的安装可能会收到网络环境的限制，
您可以尝试使用国内源进行下载安装。
```



安装ROS Noetic
------------------------

* 设置 sources.list

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

* 设置您的密钥

```bash
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```



* 确保您的 Debian 软件包索引是最新，安装ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators and 2D/3D perception。

```bash
sudo apt update
sudo apt install ros-noetic-desktop-full
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc #将此命令写入.bashrc，每次启动终端会自动运行
source ~/.bashrc
```


