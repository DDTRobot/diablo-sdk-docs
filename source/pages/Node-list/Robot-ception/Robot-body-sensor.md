# Built-in sensors of robot

```{toctree}
:maxdepth: 2
:glob:
```

In this function package, we defined four ways to publish sensor data. Since the data of the built-in sensor is sent to `Pi` via the serial ports, all the publishing methods defined here use the pointer of `diablo_ctrl_node` as a parameter to publish the data without creating a new `node`. Therefore, for the built methods in the file to work, they need to be invoked in `diablo_ctrl.cpp`.

- Robot battery information: `1Hz`
- Robot status information: `10Hz`
- Robot gyroscope information: `50Hz`
- Robot joint motor information: `10Hz`

## Invoking relationships among functions

![sensor_flow_chart](../../../_static/flow_chart/sensor_flow_chart.png)

```{warning}
Adjusting the frequency of the motor information too high could affect other data packets due to the serial port's constrained bandwidth.
```