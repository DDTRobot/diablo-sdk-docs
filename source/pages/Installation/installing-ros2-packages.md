# Install and deploy ROS2

```{toctree}
:maxdepth: 1
:glob:
```

```{contents} Contents
:depth: 2
:local:
```

## Install DIABLO_ROS2 on Sunrise X3 PI

- [Install the Sunrise X3 PI system image](https://developer.horizon.ai/resource)
- [Horizon Robotics Platform](https://developer.horizon.ai/api/v1/fileData/TogetherROS/index.html)

```{tip}
If you have installed a foxy package, but the compilation process fails to recognize it. This may be caused by soft connnection, try `source /opt/ros/foxy/setup.bash`. All hardware platform-related activities are based on Horizon's "official documentation", which is updated regularly.
```

## Install DIABLO_ROS2 on Raspberry PI

- [Ubuntu-mate](https://ubuntu-mate.org/download/arm64/jammy/)
- [Raspberry PI serial IO port configuration](./installing-sdk-on-pi)
- [Install ROS-foxy](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html)

```{warning}
The ROS installation may be affected by the network, which may cause installation problems.
```

## Compile ROS Package

1. Create ROS project folder

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

Add the following commands to `.bashrc` to ensure that you can access `ROS Robots` node over the LAN.

```bash
export ROS_DOMAIN_ID=5 
```