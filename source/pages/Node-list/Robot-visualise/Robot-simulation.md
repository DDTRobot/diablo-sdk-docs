# 机器人仿真组件

```{toctree}
:maxdepth: 2
:glob:
```

在这个模块中，我们提供了 `rviz` 的机器人数据可视化历程，以及自定义的一个遥控器插件，您可以通过启动我们提供的 `launch` 文件来启动这些功能。您可以利用 `Ros2` 的多机通信机制，在 `机器人` 端启动 `diablo_ctrl_node` ，获得机器人的控制权。在局域网内的 `PC` 端启动 `ctrl.launch.py` 进行远程遥控，以及监测数据的反馈情况。



## 快速开始

确保您已经成功编译了 `diablo_visualise` 中的内容。

```bash
ros2 launch diablo_simulation ctrl.launch.py
```

> 注：启动后您需要手动关闭 `joint state publisher` 的 UI 。否则会影响您的数值显示。

![diablo_rviz2_launch](../../../_static/diablo_rviz_launch.png)

## 仿真设计

我们在例程中同样支持了 `gazebo` 的启动。如果您有较强的开发能力，您可以自行构建机器人的平衡算法，进行后续的运动仿真工作。如果您设计出了出色的控制程序，也欢迎您联系我们，我们会根据您的完成度给予您一定的奖励。

```
ros2 launch diablo_simulation gazebo.launch.py
```

请开始你的表演~

![diablo_gazebo_launch](../../../_static/diablo_gazebo_launch.png)

