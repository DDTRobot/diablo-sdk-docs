# 树莓派配置硬串口


```{toctree}
:maxdepth: 1
:glob:
```


```{contents} 目录
:depth: 2
:local:
```

由于在树莓派中，默认会将软串口留给外部的 `IO` 引脚，但是其性能表现并不好，所以需要将默认映射到蓝牙的硬件解码串口映射到 `IO` 上。提高通信的稳定性。

## 从头开始构建

1. 下载 [Ubuntu mate](https://ubuntu-mate.org/download/) 镜像。这里我们更建议您使用对 `Ros2` 有更好支持的 64-bit 系统。

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


