# UART :
## What does UART stand for?
UART stands for Universal Asynchronous Receiver and Transmitter

## Is UART synchronous or asynchronous? Why?
UART is asynchronous because there is NO separate clock signal shared between transmitter and receiver.

## What are the minimum signals required for UART communication?
The minimum signals required for UART communication are:

1.TX (Transmit)

2.RX (Receive)

3.GND (Common Ground)

## What is a baud rate?
Baud rate is the number of bits transmitted per second in serial communication.

## If baud rate is 9600, what does it mean?
If the baud rate is 9600, it means 9600 bits are transmitted per second

## What is the difference between UART and USART?
🔹 UART

- Only Asynchronous

- ❌ No shared clock

- Uses start and stop bits

🔹 USART

- Universal Synchronous/Asynchronous Receiver Transmitter

- Can work in:

    - ✅ Asynchronous mode (like UART)

    - ✅ Synchronous mode (with clock)

- In synchronous mode:

    - ✔ Clock line is present

    - ✔ Faster and more reliable


## Why is a start bit required in UART?
The start bit is used to notify the receiver that data transmission is starting and to synchronize the receiver.

## Why is a stop bit used?
The stop bit indicates the end of the data frame and allows the receiver to return to the idle state.

## What is the typical logic level of an idle UART line?
The idle state of a UART line is LOGIC HIGH (1).

- Idle → HIGH

- Start bit → LOW

- Data bits → 0 or 1

- Stop bit → HIGH

## Can two devices with different baud rates communicate? Why?
No, two UART devices with different baud rates cannot communicate correctly.

If they try, it will lead to data corruption due to incorrect bit sampling.

## What is a UART frame format?
A UART frame format consists of a start bit, data bits, an optional parity bit, and one or more stop bits.

## Explain the role of start bit, data bits, parity bit, and stop bit in UART.
- Start bit: Indicates the beginning of data transmission and synchronizes the receiver

- Data bits: Carry the actual data being transmitted

- Parity bit: Used for simple error detection

- Stop bit: Indicates the end of the data frame

## What is the difference between even parity and odd parity?
- Even parity: The parity bit is set so that the total number of 1s (data bits + parity bit) is even.

- Odd parity: The parity bit is set so that the total number of 1s (data bits + parity bit) is odd.

## How does UART detect errors?
UART detects errors using:

1.Parity error – parity bit mismatch

2.Framing error – incorrect or missing stop bit

3.Overrun error – receiver buffer overflow

4.Break condition – line held low longer than a frame

## What is baud rate mismatch tolerance?
Baud rate mismatch tolerance is the acceptable difference between the transmitter and receiver baud rates where UART communication can still work without errors.

## What is bit time? How is it calculated?
Bit time is the time duration of one bit in UART communication.

Bit time (seconds)=1/Baud rate

## Why is UART considered full-duplex?
UART is considered full-duplex because it has separate TX (transmit) and RX (receive) lines, allowing simultaneous two-way communication.

## What is the role of TX and RX pins in UART?
- TX (Transmit) pin → Sends data from the device to another device

- RX (Receive) pin → Receives data coming from another device

## Why do we connect TX of one device to RX of another?
We connect TX of one device to RX of another because one device sends data and the other receives it, enabling proper UART communication.

## What happens if parity settings differ between devices?
If the parity settings differ between devices, the receiver may detect incorrect parity, leading to data corruption or parity errors.






# I2C 

## What is I²C? Why is it called a two-wire protocol?
I²C (Inter-Integrated Circuit) is a serial communication protocol used for communication between multiple devices on the same board.

It supports multiple masters and multiple slaves.

It is called a two-wire protocol because it uses two lines:

SDA (Serial Data Line) → used to transfer data

SCL (Serial Clock Line) → used to provide clock

The master device generates the clock and controls the communication, while the slave devices respond using their unique addresses.

I²C is a two-wire, synchronous serial communication protocol that allows multiple master and slave devices to communicate using SDA and SCL lines with address-based communication.

## Who generates the clock signal in I²C, and why is it needed?
The master device generates the clock signal on the SCL line.

The clock is required to synchronize data transfer between the master and slave, so both devices know when to sample and change data on the SDA line.

## 
