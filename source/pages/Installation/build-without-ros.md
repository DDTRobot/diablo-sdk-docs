# Compile SDK by using source code

```{toctree}
:maxdepth: 1
:glob:
```

```{contents} Contents
:depth: 2
:local:
```

You can choose to compile the SDK without dependent on `ROS`. But `SDK` still works through the serial port, please make sure your device can recognize the serial port.

## Compile static link library

```bash
git clone https://github.com/DDTRobot/diablo-sdk-v1.git
cd diablo-sdk-v1
vi CMakeLists.txt

#Set WITH_ROS to 0
set(WITH_ROS  0)

mkdir build && cd build
cmake .. 
make 
```

You will get a static link library of `libdiablo_sdk.a` after completion of compilation.