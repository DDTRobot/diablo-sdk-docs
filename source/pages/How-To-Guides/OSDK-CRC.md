# CRC Verification

```{toctree}
:maxdepth: 2
:glob:
```

```{contents} Contents
:depth: 2
:local:
```

------

## ` bool   verify_crc16(const void* data, size_t len);`

- brief:  Verify CRC16 value of a received data packet.

- param:

- return：True if CRC value is correct.

- note:   NON-API FUNCTION.

## ` uint16_t  update_crc16(const void* data, size_t len);`

- brief:  Calculate CRC16 value of a data packet.

- param: Shall equal to sizeof(packet) - 2.

- return: CRC code.

- note:   NON-API FUNCTION.