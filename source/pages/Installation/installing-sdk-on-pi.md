# Raspberry PI serial IO port configuration

```{toctree}
:maxdepth: 1
:glob:
```

```{contents} Contents
:depth: 2
:local:
```

In Raspberry PI, by default, the soft serial port is reserved for the external `IO` pins, but their performance is not very good. Therefore, the hardware decoding serial port mapped to Bluetooth by default needs to be mapped to `IO`. Improve the stability of communication.

## Build from scratch

1. Download [Ubuntu mate](https://ubuntu-mate.org/download/) image here. Here, we recommend that you use a 64-bit system with better support to `ROS2`.

#### 1\. Start Serial0

- There are two default serial ports in Raspberry PI, one is the software serial port `ttyS0` and the other is the hardware serial port `ttyAMA0`. By default, `Serial0` is not enabled. By default, the more stable hardware serial port `ttyAMA0` is used for onboard Bluetooth communication `Serial1`. You can view the corresponding serial port mapping information by using the following commands.

```bash
ls -l /dev/serial*
#/dev/serial1 -> ttyAMA0
```

- First, you need to enable `Serial0` in the configuration file. Modify the serial port enable configure information in `/boot/firmware/config.txt` and `/boot/firmware/syscfg.txt`.

```bash
#enable_uart=0
enable_uart=1
```

#### 2\. Modify the mapping relationship

- Our goal is to use the IO serial port in the Raspberry PI. However, currently `Serial0` is mapped to the software serial port, therefore, it is necessary to map the more stable hardware serial port `ttyAMA0` to `Serial0`.

```bash
ls -l /dev/serial*
#serial0->ttyS0
#serial1->ttyAMA0
```

- Add a line `/boot/firmware/config.txt` at the end to turn off the onboard Bluetooth.
 
```bash
dtoverlay=disable-bt
```

```bash
sudo systemctl disable bluetooth
```

Restart the device, the IO mapping has been reversed now. You can operate `ttyAMA0`, and the output signal will be sent through the onboard `IO`.

```bash
ls -l /dev/serial*
#serial0->ttyAMA0
#serial1->ttyS0
```

### 3\. Modify serial port permissions

- By default, the serial ports of `ttyAMA0` need root privileges to be invoked. Therefore, we need to add our user to the `dialout` user group.

```bash
 sudo apt install rpi.gpio-common
 sudo adduser ${USER} dialout   #Replace the output user name ${USER}
 sudo reboot
```