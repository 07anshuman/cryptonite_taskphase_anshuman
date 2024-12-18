# Serial Communication Protocols

## UART (Universal Asynchronous Receiver Transmitter)

 - Asynchronous meaning no shared clock line b/w receiver and trasnmitter, so there has to be another mechanism in place to know the beginning and end of reception. 

 - By default (when no transmission) the signal is high, and the first bit (the start bit) is `0` which marks the beginning of communication. This is followed by 8 bits of data (generally) and a stop bit. 

```
5 bits: Used for older protocols, like teletype (TTY) machines.
7 bits: Often used for ASCII character transmission, as ASCII fits within 7 bits.
8 bits: Default and most common, supports extended ASCII and binary data.
9 bits: Used in applications that require additional control information or specialized protocols.
```

- The transmission and reception rate of bits (baud rate) must be nearly equal (within 2%) to have a readable reception. The baud rate is the number of bits transmitted in each sec and is calculated to be inverse of the time of the smallest bit, that way it can read all bits.

- Simple to implement, slow

## I2C (Inter-Integrated Circuit)

 - Synchronous communication protocol meaning a separate shared clock line exists. The clock input is created simultaneously with the data and is of the same frequency as the bits of the data. The baud rate is communicated this way.

 - It is a multi-master multi-slave communication protocol. When multiple slave devices are connected a slave address is sent at the start to know which slave is supposed to store this data. 

 - After each byte, the receiver sends an ACK (acknowledge) bit to confirm successful reception. I2C is also half duplex meaning data can flow in only one direction at a time.

 - The extra overhead in UART reduces the effective data rate compared to I²C. No start/stop bit; tightly synchronized.

# Serial Peripherical Interface (SPI)

 - synchronous, full-duplex communication protocol, single master multi-slave
 - Separate lines for transmitting and receiving. MISO (Master Input Slave Output), MOSI (Master Output Slave Input), SCLK (Serial Clock), SS (Slave Select).
 - Much faster than UART or I2C. No start/stop bits or acknowledgment bits like in UART or I²C.
 - At least four pins (SCLK, MOSI, MISO, SS) are needed, and additional pins are required for each slave device.
 - not ideal for long-distance communication as multiple wires needed

