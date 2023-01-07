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
rosrun diablo_sdk virtual_rc_example
```

## Run SDK demo

Run `./script/teleop.py` script from the control side.

You can also use ` ROS` multi-machine communication ability to control the robot remotely.

### Operating instruction

`w`: control the robot to move forward  
`s`: control the robot to move backward  
`a`: Control the robot to turn left  
`d`: Control the robot to turn right  
`z`: Switch the robot to standing mode  
`x`: Switch the robot to creeping mode  
`q`: Control the robot to tilt to the left (standing mode)  
`e`: Control the robot to tilt to the right (standing mode)  
`c`: Switch the robot to motion mode (faster movement speed, allowing jumping in standing mode)  
`v`: Switch the robot to show mode (smooth movement speed, jumping is not allowed)  
`r`: Control the robot to jump while standing mode and in motion  
`1`: Exit virtual remote control.

```{note}
Please don't change the remote control mode while the virtual remote control is in use for your safety. Please switch the robot to creeping mode and configure the robot to creeping mode via the remote control before disconnecting the virtual remote control. You can utilize the physical remote control handle to protect your robot while debugging, since it has a greater level of control authority than the virtual handle.
```

```{warning}
When the robot is put in standing mode, an overload will activate the generator protection program, which will prohibit the robot from standing up and a severe overload will activate the battery protection program, which will cut off the power. When the maximum load is reached,please do not switch the robot mode for safety.
```