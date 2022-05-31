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
sudo apt install ros-noetic-ros-base
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc #将此命令写入.bashrc，每次启动终端会自动运行
source ~/.bashrc
```

## 安装 wiringpi 串口库

- `wiringPi` 是树莓派提供的控制 `IO` 的库。树莓派通过 `IO` 的串口与 `MUC` 相连，由于 `wiringPi` 的兼容性，您只能在支持此库的设备中使用 API 或者将串口库替换成支持您自己平台的库。

```
cd /tmp
wget https://project-downloads.drogon.net/wiringpi-latest.deb
sudo dpkg -i wiringpi-latest.deb
```


