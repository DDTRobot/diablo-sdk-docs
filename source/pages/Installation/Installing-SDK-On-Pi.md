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
	#/dev/serial0 -> ttyS0
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
	whoami 	#diablo  获得用户名
	sudo usermod -aG dialout diablo 	#将当前用户添加到dialout用户组。
 ```



## 通过我们的镜像开始构建

