# The robot obtains the SDK control permission

```{toctree}
:maxdepth: 2
:glob:
```

This is the basic node for robot control. You need to run `diablo_ctrl_node` to obtain the control permission of the robot. To gain control, you should send your control command to `/diablo/MotionCmd` in a custom msg `MotionCtrl`.  

## Serial port modification

By default, the robot uses `x3 pi` on-board io `/dev/ttyS3` for serial communication. If you need to modify it, please adjust to the corresponding serial port number and recompile.

```c++
 //file：diablo_ctrl.cpp
 Hal.init("/dev/ttyS3")
```

## Control instructions

| Control ID| Value range| Remark|
|:----------|----------|----------|
| CMD_GO_FORWARD(0x08)| ±2.0 m/s| Negative numbers indicate backward movement|
| CMD_GO_LEFT(0x04)| ±2.0 rad/s| Negative numbers indicate movement to the right|
| CMD_ROLL_RIGHT(0x09)| ±0.2 rad| Negative numbers indicate movement to the left|
| CMD_STAND_UP(0x02)| 0.0| Robot in standing mode|
| CMD_STAND_DOWN(0x12)| 0.0| Robot in squat mode|
| | | |
| CMD_PITCH_MODE(0x13)| (0.0，1.0)| Position mode 0, speed mode 1|
| CMD_PITCH(0x03)| ±0.3 pi| Position mode 0|
| CMD_PITCH(0x03)| ±1.2 rad/s| Speed mode 1|
| | | |
| CMD_HEIGH_MODE(0x01)| (0.0，1.0)| Position mode 0, speed mode 1|
| CMD_BODY_UP(0x11)| 0.0~1.0| Position mode 0|
| CMD_BODY_UP(0x11)| ±0.5 m/s| Speed mode 1|

> In the speed mode, the robot will keep moving at the speed specified in the command.
> 
> In the position mode, the robot will move in a fixed position represented by the value from the command.

## Invoking relationships 

![ctrl_flow_chart](../../../_static/flow_chart/ctrl_flow_chart.png)

```{warning}
By changing the areas of `diablo ctrl.cpp` that are commented out, you can change the robot's top speed. This setting will be in effect until the robot is shut off. You can configure this node to auto startup. This can alter the speed controlled by the remote control.

//vehicle.telemetry->setMaxSpeed(1.0);   
The upper limit is 2.0; exceeding this speed could harm your robot permanently.
```