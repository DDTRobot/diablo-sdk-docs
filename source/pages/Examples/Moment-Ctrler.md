# Raspberry PI OS image flash tutorial

```{toctree}
:maxdepth: 1
:glob:
```

```{contents} Contents
:depth: 2
:local:
```

## Install balenaEtcher and start it on Windows

```bash
roscore &
rosrun diablo_sdk movement_ctrl_example
```

## Run SDK demo

Run `./script/teleop.py` script from the control side. Used for capturing the keyboard input and forward it to its control node via `Ros`.

You can also use ` ROS` multi-machine communication ability to control the robot remotely.

### Operating instruction

`w`: Control the robot to move forward. `Low-speed mode::` (-1.0~+1.0 m/s); `High-speed mode::` (-1.6~+1.6 m/s)

`s`: Control the robot to move backward. `Low-speed mode::` (-1.0~+1.0 m/s); `High-speed mode::` (-1.6~+1.6 m/s)

`a`: Control the robot to turn left. `Arbitrarily mode::` (-5.0~+5.0 rad/s)

`d`: Control the robot to turn right. `Arbitrarily mode::` (-5.0~+5.0 rad/s)

`q`: Control the robot to tilt to the left. `Standing mode::` (-0.2~+0.2 rad/s)

`e`: Control the robot to tilt to the right. `Standing mode::` (-0.2~+0.2 rad/s)

`r`: Adjust the tilt angle of the fuselage to horizontal. `Standing mode:`

`v`: Switch the robot to the standing mode.

`z`: Switch the robot to creeping mode.

`n`: Control mode for raising the robot. `Position mode 0:` (0 ~ 1)

`m`: Control mode for raising the robot. `Position mode 1:` (-0.25 ~ +0.25 m/s)

`f`: Minimum height in standing mode. `Position mode`

`g`: Middle height in standing mode. `Position mode`

`h`: Maximum height in standing mode. `Position mode`

`x`: Reduced the fixed speed to the minimum. `Speed mode`

`c`: Increase the fixed speed to the maximum. `Speed mode`

`y`: Control mode for raising the robot. `Position mode 0:` (-0.3 ~ +0.3 pi)

`u`: Control mode for raising the robot. `Speed mode 1:` (-1.8 ~ +1.8 rad/s)

`1`: Exit virtual remote control.

```{note}
Please don't change the remote control mode while the virtual remote control is in use for your safety. Please switch the robot to creeping mode and configure the robot to creeping mode via the remote control before disconnecting the virtual remote control. You can utilize the physical remote control handle to protect your robot while debugging, since it has a greater level of control authority than the virtual handle.
```

```{warning}
When the robot is put in standing mode, an overload will activate the generator protection program, which will prohibit the robot from standing up and a severe overload will activate the battery protection program, which will cut off the power. When the maximum load is reached,please do not switch the robot mode for safety.
```