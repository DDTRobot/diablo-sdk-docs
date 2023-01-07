# Rviz2 custom plug-in of robot

```{toctree}
:maxdepth: 2
:glob:
```

In this function package, we created a remote control visualization plug-in for `Rviz2` by utilizing `Qt`. You can also use this routine as a reference to modify its control logic, or customize some data visualization plug-ins, which may require you to have some knowledge of `Qt`.

## Plug-in preview

![rviz_plugin](../../../_static/rviz_plugin.png)

## Quick start

Make sure you have successfully compiled the nodes in `diablo_rviz2_plugin`.

> - Panels -> Add new panel -> mission panel

Before use, you need to start `diablo_ctrl_node` from `Robot end` to obtain the control permission of the robot. Then search for `/diablo/MotionCmd` by clicking `Detect` to establish a control connection.

You can control the robot standing height by dragging the right `Slider`. Adjust the values in the window to change the robot's control speed. You can control it by clicking on the UI button using a mouse. You can also hover the cursor over this component and use the keyboard to control it.

| q (tilt left)| w (go forward)| e (tilt left)|
|:----------:|:----------:|:----------:|
| a (turn left)| s (go backward)| d (turn right)|
| z (head up at a fixed speed)| x (stop head up or tilting)| c (head down at a fixed speed)|

## Thanks

- [Cyberdog_rviz2_plugin](https://github.com/linzhibo/Cyberdog_rviz2_plugin)