# Install and deploy ROS

```{toctree}
:maxdepth: 1
:glob:
```

```{contents} Contents
:depth: 2
:local:
```

## Install ROS-noetic on Raspberry PI

- [Install Ubuntu mate](https://ubuntu-mate.org/download/arm64/jammy/)
- [Raspberry PI serial IO port configuration](./installing-sdk-on-pi)
- [Install ROS-noetic](http://wiki.ros.org/noetic/Installation/Ubuntu)

The installation of ROS may be affected by the network and result in problems.

## Compile ROS Package

1. Create ros project folder

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

Add the following commands to `.bashrc` to ensure that you can access `ROS Robots` node over the LAN.

```bash
export ROS_IP=${On-board Raspberry PI IP}
export ROS_MASTER_URI=http://${ROS_IP}:11311
```