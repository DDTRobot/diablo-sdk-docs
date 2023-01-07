# On-board sensor interface of the robot

```{toctree}
:maxdepth: 2
:glob:
```

This directory defines the interface through which the information of the various sensors reported by the `MCU` is published in `ROS2`. Use `ROS2` built-in message format first, which makes it easier to use some of the visualization functions in `ROS2`.

## Message Introduction

- Robot motor information x6
  
  > - Message header
  > - Number of windings of motor
  > - Motor angle
  > - Motor speed
  > - Torque current
  > - The vertical distance between the shaft center of the outer motor and the shaft center of the hub motor

- Movement control command
  
  > - Control instruction
  > 
  > - Control value

- Robot control status information
  
  > - Control mode
  > 
  > - Robot motion status code
  > 
  > - Error message
  > 
  > - Warning message