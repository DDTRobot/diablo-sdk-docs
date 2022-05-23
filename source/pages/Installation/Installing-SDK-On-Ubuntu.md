# 在Ubuntu上部署DIABLO-SDK

```{toctree}
:maxdepth: 1
:glob:
```

```{contents} 目录
:depth: 2
:local:
```

本页介绍如何在Ubuntu Linux系统中构建 DIABLO-SDK。您需要将我们提供的SDK在您的ROS工作空间中进行编译。



创建ROS工作空间
----------------

```bash
  mkdir -p catkin_ws/src    #创建一个工作空间的文件夹
  cd catkin_ws/src          #进入Src目录
  catkin_init_workspace     #初始化ROS工程
  cd ..                     #回到catkin_ws目录
  catkin_make               #编译项目
  source devel/setup.bash
```

## 获取DIABLO-SDK

进入src目录，并获取官方SDK源码。

```bash
 cd catkin_ws/src
 git clone https://gitee.com/direct-drive-tech/diablo-onboard-sdk.git
```

安装Ros串口支持包

```bash
  cd catkin_wx/src/diablo-onboard-sdk/serial
  mkdir Build
  cd Build
  cmake ..
  make
  sudo make install 
```


```{note}
  在 cmake 的过程中若出现找不到 ``catkin_DIR`` 等问题可能是您没有安装好ROS，或是没有 ``source devel/setup.bash``。
  可以尝试 ``source devel/setup.bash`` 后再次编译。若出现一切有关于依赖保安装的未知问题，可以使用 ``apt install`` 命令尝试进行安装。
```

修改CMakeList配置

```bash
  cd catkin_wx/src/diablo-onboard-sdk/
  vi CMakeLists.txt

  '''
  修改文件中的配置信息如下

  set(WITH_ROS    1)
  set(WITH_SERIAL 1)
  set(WITH_PI     0)
  set(WITH_LOG_FILE 0)
  set(WITH_CONSOLE_LOG 0)
  '''

  '''
  若不需要ROS进行编译，您可以使用如下配置

  set(WITH_ROS    0)
  set(WITH_SERIAL 1)
  set(WITH_PI     0)
  set(WITH_LOG_FILE 0)
  set(WITH_CONSOLE_LOG 0)
  '''
  
  cd catkin_wx
  catkin_make
  source devel/setup.bash
```


## 配置ROS远程通信

编辑向`.bashrc`添加以下指令，保证您可以通过局域网访问`ROS机器人` 的节点。

```bash

export ROS_IP=${机载树莓派IP}
export ROS_MASTER_URI=http://${ROS_IP}:11311

```

