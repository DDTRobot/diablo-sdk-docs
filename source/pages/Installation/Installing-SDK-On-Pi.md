# 在树莓派中部署DIABLO-SDK


```{toctree}
:maxdepth: 1
:glob:
```


```{contents} 目录
:depth: 2
:local:
```

本页介绍如何在树莓派中构建 DIABLO-SDK。您可以通过自己的方式从头开始构建自己的镜像，也可以使用我们构建好的镜像，但这需要您的SD卡容量需要大于或等于32GB。

## 从头开始构建

1. 下载 [Ubuntu mate](https://ubuntu-mate.org/download/armhf/focal/thanks/?method=torrent) 镜像。这里我们选择使用了32位的 Ubuntu 20.04的系统。
2. 将 [Ubuntu mate](https://ubuntu-mate.org/download/armhf/focal/thanks/?method=torrent) 镜像参照[镜像刷写教程](./Flash-image)进行镜像的刷写。
3. 安装 [Ros Noetic](./Build-Dependencies.md) ，您可以根据自己的需求选择需要的 Ros 软件包。

### 树莓派Ubuntu mate硬件串口映射到IO

  #### 一、启动Serial0
 - 树莓派中有两个默认串口，一个是软串口`ttyS0`，一个是硬件串口`ttyAMA0` 。在默认情况下 `Serial0` 是不开启的。而更加稳定的硬件串口`ttyAMA0` 则默认用于板载蓝牙的通信 `Serial1` 。您可以通过以下指令查看对应的串口映射信息。
 ```bash
	ls -l /dev/serial*
	#/dev/serial1 -> ttyAMA0
 ```
- 首先您需要先在配置文件中打开 `Serial0`。
  在 `/boot/firmware/config.txt` 与 `/boot/firmware/syscfg.txt`中修改串口使能配置信息。
 ```bash
	#enable_uart=0
	enable_uart=1
 ```
配置完成后重启，重启后再次使用查看映射信息，可以发现 `Serial0` 已经打开了。

 #### 二、修改映射关系
  - 我们的目的是使用树莓派中的IO串口。因此需要将更加稳定的硬件串口`ttyAMA0` 映射到 `Serial0` 中，而目前 `Serial0` 是映射到软串口中的。
 ```bash
	ls -l /dev/serial*
	#serial0->ttyS0
	#serial1->ttyAMA0
 ```
-  在 `/boot/firmware/config.txt` 末尾追加一行，来关闭板载的蓝牙。
 ```bash
	dtoverlay=disable-bt
 ```

 ```bash
	sudo systemctl disable bluetooth
 ```
重启设备，目前 IO 的映射就已经对调了。您可以通过对 `ttyAMA0` 进行操作，输出信号将会通过板载的 `IO` 进行发送。
 ```bash
	ls -l /dev/serial*
	#serial0->ttyAMA0
	#serial1->ttyS0
 ```

 ### 三、修改串口权限

- 在默认情况下 `ttyAMA0` 的串口是需要 root 权限才可以调用的。所以我们需要将自己的用户添加到 `dialout` 的用户组中。

 ```bash
  sudo apt install rpi.gpio-common
  sudo adduser ${USER} dialout   #将输出的用户名替换${USER}
  sudo reboot
 ```


### 四、创建ROS工作空间

```bash
  sudo apt install git tree openssh-server
  mkdir -p catkin_ws/src    #创建一个工作空间的文件夹
  cd catkin_ws/src          #进入Src目录
  catkin_init_workspace     #初始化ROS工程
  git clone https://github.com/Direcrt-Drive-Technology/diablo-sdk-v1.git
  cd ..                     #回到catkin_ws目录
  catkin_make               #编译项目
  source devel/setup.bash
```

```{note}
  在 cmake 的过程中若出现找不到 ``catkin_DIR`` 等问题可能是您没有安装好ROS，或是没有 ``source devel/setup.bash``。
  可以尝试 ``source devel/setup.bash`` 后再次编译。若出现一切有关于依赖保安装的未知问题，可以使用 ``apt install`` 命令尝试进行安装。
```

### 五、只编译SDK部分

我们的 `SDK` 支持您脱离 `Ros` 进行编译，这有助于您适配自己的代码，或是在自定义您自己 `API` 的过程中提供更好的编译体验。


