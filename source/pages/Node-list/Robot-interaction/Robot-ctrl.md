# 机器人获取SDK控制权限

```{toctree}
:maxdepth: 2
:glob:
```

此节点是机器人控制的基础节点，您需要运行 `diablo_ctrl_node` 获取机器人的控制权限。您可以将您的控制指令以自定义msg : `MotionCtrl` 的格式发送到 `/diablo/MotionCmd` 实现控制效果。



## 串口修改

机器人默认使用 `x3 pi` 的板载 io `/dev/ttyS3` 进行串口通信，如果您需要对其进行修改，请调整至对应的串口号，并重新编译。

```c++
 //file：diablo_ctrl.cpp
 Hal.init("/dev/ttyS3")
```



## 控制指令

| 控制ID               | 数值范围   | 备注                 |
| :------------------- | ---------- | -------------------- |
| CMD_GO_FORWARD(0x08) | ±2.0 m/s   | 负数为向后运动       |
| CMD_GO_LEFT(0x04)    | ±2.0 rad/s | 负数为向右运动       |
| CMD_ROLL_RIGHT(0x09) | ±0.2 rad   | 负数为向左运动       |
| CMD_STAND_UP(0x02)   | 0.0        | 机器人站立           |
| CMD_STAND_DOWN(0x12) | 0.0        | 机器人下蹲           |
|                      |            |                      |
| CMD_PITCH_MODE(0x13) | (0.0，1.0) | 位置模式0，速度模式1 |
| CMD_PITCH(0x03)      | ±0.3 pi    | 位置模式0            |
| CMD_PITCH(0x03)      | ±1.2 rad/s | 速度模式1            |
|                      |            |                      |
| CMD_HEIGH_MODE(0x01) | (0.0，1.0) | 位置模式0，速度模式1 |
| CMD_BODY_UP(0x11)    | 0.0~1.0    | 位置模式0            |
| CMD_BODY_UP(0x11)    | ±0.5 m/s   | 速度模式1            |

> 速度模式，机器人将以指令中数值的速度持续运动。
>
> 位置模式，机器人将以指令中数值代表的固定位置运动。



## 调用关系

![ctrl_flow_chart](../../../_static/flow_chart/ctrl_flow_chart.png)

```{warning}
您可以修改 `diablo_ctrl.cpp` 中被注释的部分，来修改机器人的最大速度。此设置在机器人断电之前会一直生效，您可以将此节点设置为开机启动。这可以改变遥控器的控制速度。

//vehicle.telemetry->setMaxSpeed(1.0);   
上限为：2.0，过大的速度可能会对您的机器人造成不可逆损坏！！！
```

