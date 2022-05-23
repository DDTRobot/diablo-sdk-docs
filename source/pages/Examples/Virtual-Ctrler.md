# 虚拟遥控器案例

```{toctree}
:maxdepth: 1
:glob:
```

虚拟遥控器控制脚本存放于控制端`./script`文件夹下。

## 环境依赖

```bash
pip install rospy pygame pyautogui
```

```{note}
如通过机载树莓派运行控制脚本，遇到`pygame，pyautogui`安装出错等问题，你可以尝试更换国内源，或是在PC上运行脚本，通过 `ros` 多机之间通信以进行虚拟遥控器控制。
```

您可以通过[在Ubuntu上部署DIABLO-SDK](../Installation/Installing-SDK-On-Ubuntu.md)中的教程部署SDK。部署完成后运行 ` roscore`，并启动控制节点。

```bash
roscore
rosrun diablo_sdk virtual_rc_example
```

## 运行SDK演示案例

在控制端，运行 `./script/teleop.py` 脚本。

若是多机通信，则启动`ros`后需设置完成`ros`[远程通信](../Installation/Installing-SDK-On-Ubuntu.md)，再运行SDK案例和控制脚本。

### 操作说明

 `w` : 控制机器人向后移动  
 `s` : 控制机器人向后移动  
 `a` : 控制机器人向左转向  
 `d` : 控制机器人向右转向  
 `z` : 切换机器人至站立形态  
 `x` : 切换机器人至匍匐形态  
 `q` : 控制机器人向左倾斜(站立模式)  
 `e` : 控制机器人向右倾斜(站立模式)  
 `c` : 切换机器人至运动模式(更快的移动速度，站立形态下允许跳跃)  
 `v` : 切换机器人至展示模式(平稳的移动速度，禁止跳跃)  
 `r` : 运动模式站立形态下控制机器人跳跃  
`esc`: 退出虚拟遥控器控制。

```{note}
为安全起见，请不要在虚拟遥控器操控时切换遥控器模式，断开虚拟遥控器前请切换机器人为匍匐形态且遥控器设置机器人为匍匐形态。 
```

```{warning}
切换机器人为站立模式时，若负载过大会触发电机保护程序，将阻止机器人站起，若严重过载将触发电池保护程序，电池将断开供电。为安全起见，请勿超过最大负载切换机器人形态。
```




