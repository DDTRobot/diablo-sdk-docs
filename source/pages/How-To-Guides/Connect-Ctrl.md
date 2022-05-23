# 通信协议

```{toctree}
:maxdepth: 2
:glob:
```

```{contents} 目录
:depth: 2
:local:
```
------

## ` struct  OSDK_Uart_Header_t`

```c++
uint8_t   SOF;          //starting byte, fixed to be 0xAA
uint16_t  LEN : 10;     //len of frame
uint16_t  VERSION : 6;  //version of the frame header, set to be 0
uint8_t   SESSION : 5;  //session ID, 0: Sender doesn't need ACKs. 1:Sender needs ACKs but can be tolerated. 2:Sender needs ACKs.*
uint8_t   ACK : 1;      //frame type, 0: CMD, 1:ACK
uint8_t   RES0 : 2;
uint8_t   PADDING : 5;  //len of padding data used by the Data encryption
uint8_t   ENC : 3;      //encryption type, 0: no encryption, 1: AES encryption
uint8_t   RES1[3];
uint16_t  SEQ;          //frame sequence num
uint16_t  CRC16;        //CRC16 frame header checksum
```


## ` struct  OSDK_Uart_Packet_t`

```c++
OSDK_Uart_Header_t header;   //CRC16 frame header checksum
uint8_t   CMD_SET;           //0x00, Initialization, 0x01, Control, 0x02, Push Data
uint8_t   CMD_ID;
void*     DATA;              //Pointer to data
uint16_t  CRC16;             //CRC32 whole frame checksum
```

## ` struct  OSDK_ACK_t`

```c++
uint8_t   cmd_set;       //equal to cmd set value of message that triggers ack
uint8_t   cmd_id;        //equal to cmd id value of message that triggers ack
uint16_t   VAL;
```

## ` struct  OSDK_Uart_ACK_Packet_t`

```c++
OSDK_Uart_Header_t header;    //CRC16 frame header checksum
OSDK_ACK_t  ACK;              //ACK value
uint16_t  CRC16;              //CRC32 whole frame checksum
```

## ` struct  OSDK_Movement_Ctrl_Mode_t`

```c++
uint16_t  reserve_mode : 11;            //reserved for further use
uint8_t	  head_controller_mode : 1;     //1:head stable    0: head assist balance
uint8_t   yaw_ctrl_mode : 1;            //1:control angle  0: control angular velocity
uint8_t	  plit_ctrl_mode : 1;           //1:control angle  0: control angular velocity
uint8_t	  pitch_ctrl_mode : 1;          //1:control angle  0: control angular velocity
uint8_t	  roll_ctrl_mode : 1;           //1:control angle  0: control angular velocity
uint8_t	  height_ctrl_mode : 1;         //1:control height 0: control vertical velocity
```

## ` struct  OSDK_Movement_Ctrl_t`

```c++
float        forward;
float           left;
float             up;
float           roll;
float          pitch;
float      leg_split;

```

## ` struct  OSDK_Virtual_RC_Request_t`

```c++
uint8_t  request     :  1;      //1: Request open, 0: Request close
uint8_t  timeout_act :  1;      //Action after drop connection, 1:Automatically switches to real remote control
                                //0 No switches，execute disconnect program
uint16_t timeout_ms  : 14;      //automatic release control authority after timeout ms  

```

## ` struct  OSDK_Virtual_RC_t`

```c++
    uint16_t ch1;           //channal value 200-1800
    uint16_t ch2;
    uint16_t ch3;
    uint16_t ch4;
    uint16_t ch5;
    uint16_t ch6;
    uint16_t ch7;
    uint16_t ch8;
    uint16_t ch9;
    uint16_t ch10;
    uint16_t ch11;
    uint16_t ch12;
    uint8_t  ch13     : 1;
    uint8_t  ch14     : 1;
    uint8_t  ch15     : 1;
    uint8_t  ch16     : 1;
    uint8_t  ch17     : 1;
    uint8_t  ch18     : 1;
    uint8_t  ch19     : 1;
    uint8_t  failsafe : 1;

```


## ` struct  OSDK_Push_Data_Freq_Select_t`

```c++
    OSDK_PUSH_DATA_OFF        = 0,
    OSDK_PUSH_DATA_1Hz        = 1,
    OSDK_PUSH_DATA_10Hz       = 2,
    OSDK_PUSH_DATA_50Hz       = 3,
    OSDK_PUSH_DATA_100Hz      = 4,
    OSDK_PUSH_DATA_500Hz      = 5,
    OSDK_PUSH_DATA_1000Hz     = 6,
    OSDK_PUSH_DATA_NO_CHANGE  = 7,

```


## ` struct  OSDK_Push_Data_Flag_t`
```c++
    uint8_t  status      : 1; 
    uint8_t  quaternion  : 1; 
    uint8_t  accl        : 1;
    uint8_t  gyro        : 1;
    uint8_t  RC          : 1;
    uint8_t  power       : 1;
    uint8_t  motor       : 1;
    uint16_t reserve     : 9;

```

## ` enum    OSDK_Ctrl_Mode_t`

```c++

    OSDK_CTRL_MODE_RC          = 0,
    OSDK_CTRL_MODE_MOTION      = 1,
    OSDK_CTRL_MODE_VIRTUAL_RC  = 2

```


## ` enum    OSDK_Robot_State_t`

```c++

    OSDK_ROBOT_STATE_DISCONNECT      = 0,
    OSDK_ROBOT_STATE_INITIALIZE      = 1,
    OSDK_ROBOT_STATE_CAR             = 2,
    OSDK_ROBOT_STATE_STAND           = 3,
    OSDK_ROBOT_STATE_TRANSITION_DOWN = 4,
    OSDK_ROBOT_STATE_TRANSITION_UP   = 5

```

## ` struct  OSDK_Push_Data_Status_t`

```c++
    uint8_t  ctrl_mode;
    uint8_t  robot_mode;
    uint64_t error;
    uint64_t warning;

```

## ` struct  OSDK_Push_Data_Quaternion_t`

```c++
    float w;
    float x;
    float y;
    float z;

```

## ` struct  OSDK_Push_Data_XYZ_t`

```c++

    float x;
    float y;
    float z;

```

## ` struct  OSDK_Push_Data_RC_t`

```c++

    uint32_t ch1  : 11;
    uint32_t ch2  : 11;
    uint64_t ch3  : 11;
    uint32_t ch4  : 11;
    uint32_t ch5  : 11;
    uint32_t ch6  : 11;
    uint32_t ch7  : 11;
    uint32_t ch8  : 11;
    uint32_t ch9  : 11;
    uint32_t ch10 : 11;
    uint32_t ch11 : 11;
    uint32_t ch12 : 11;
    uint32_t ch13 : 11;
    uint32_t ch14 : 11;
    uint32_t ch15 : 11;
    uint32_t ch16 : 11;
    uint8_t  ch17 : 1;
    uint8_t  ch18 : 1;
    uint8_t  frame_lost : 1;
    uint8_t  failsafe   : 1;
    uint8_t  reserve    : 4;

```

## ` struct  OSDK_Push_Data_Power_t`

```c++
    float   voltage;
    float   current;
    float   capacitor_energy;
    uint8_t power_percent;

```

## ` struct  OSDK_Push_Data_M15_t`

```c++
    int32_t  enc_rev;
    uint16_t enc_pos;
    uint16_t enc_vel;
    uint16_t iq;

```

## ` struct  OSDK_Push_Data_Motor_t`

```c++
    OSDK_Push_Data_M15_t    left_hip;
    OSDK_Push_Data_M15_t    left_knee;
    OSDK_Push_Data_M15_t    left_wheel;
    OSDK_Push_Data_M15_t    right_hip;
    OSDK_Push_Data_M15_t    right_knee;
    OSDK_Push_Data_M15_t    right_wheel;

```