# Robot motor angle conversion

```{toctree}
:maxdepth: 2
:glob:
```

Robot's legs form a parallelogram structure, but a parallel structure cannot be expressed in `xacro`. Therefore, we use angle calculations to compensate for the rotation of parallelogram structure formed by the legs.

## Calculation method

Where `l_angleB` is the angle of separation between the big leg and the midline.

In the data, `left_leg_length` is the vertical distance between `Outer motor shaft center` and `Wheel hub motor shaft center` calculated by the robot using the motor angle

```
l_angleB = (3.14 - acos( (3.92 -((msg->left_leg_length * 10)* (msg->left_leg_length*10)))/ 3.92))/2
```