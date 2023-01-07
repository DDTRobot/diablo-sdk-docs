> # Welcome to DIABLO-Development Documentation!

```{toctree}
:maxdepth: 1
:caption: DIABLO-Development-Doc
pages/Installation
pages/Node-List
```

## Introduction

![diablo_robot_render](./_static/diablo_robot_render.jpg)
In order to provide you with more choices, we offer three development methods. You can use `ROS`, `ROS2`, or directly compile the source code of the `SDK` for the secondary development of robot. We recommend you use `ROS2` for development, which delivers better performance and more stable control methods.

In the future, we will also provide more `ROS2` function packs to help you quickly obtain more functions, hoping that it can provide some help for you to customize your own robot.

* Excellent compatibility: The software design is not heavily dependent on developing environment, and you can use it on most `Linux` devices that support serial ports.

* Simple control interface: We provide the robot visualization capabilities of `rviz2` and `gazebo` in the function package of `ROS2`, which can be controlled by a customizable remote control plug-in.

* Better safety: Our system is equipped with a variety of safety assurance logics, which ensures safety to its best ability under various special conditions in the development process.

For more introduction, please visit our official website: [Direct Drive Technology](https://directdrive.com)。

### How to get started

There are three methods for compiling our `SDK`。

- [Compile the function package in ROS2 (Recommended)](./pages/Installation/installing-ros2-packages)
- [Compile the function package in ROS](./pages/Installation/installing-ros-packages)
- [Compile with C++ ](./pages/Installation/build-without-ros)

### SDK quick start

We provide you with a `Python` control node for keyboard event capture. After starting `diablo_ctrl_node` and gaining control of `SDK`, you can run `teleop_node` to capture events of the keyboard. You can refer to the usage of its commands.

```{note}
  We will be committed to providing you with more high-quality robot control services, relying on our robot platform to adapt more intelligent algorithms. We hope our effort will facilitate your development.
```