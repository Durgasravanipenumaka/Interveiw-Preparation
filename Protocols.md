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

I²C is a two-wire synchronous serial communication protocol that allows multiple slave devices to communicate with a master using SDA and SCL lines with address-based communication.

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

## What is the purpose of pull-up resistors in I²C lines (SDA and SCL)?
In I²C, the SDA and SCL lines are open-drain (open-collector).

- What does open-drain mean?

  Devices cannot drive the line HIGH

  Devices can only:

       - Pull the line LOW

       - Or release the line

So, without pull-up resistors, the line would float and logic HIGH would never be achieved.

Pull-up resistors are required in I²C because SDA and SCL are open-drain lines; they pull the lines to logic HIGH when no device is driving them LOW, ensuring reliable communication.

## Is I²C synchronous or asynchronous?
Synchronous, because communication uses a clock signal (SCL).

## What is master and slave?

Master → Initiates communication, generates clock

Slave → Responds to master using its address

## Can there be multiple masters?

Yes, I²C supports multi-master, but it is rarely used in practice.

## What is I²C addressing?

Each slave has a unique address so the master can identify it.

## 7-bit vs 10-bit addressing?

7-bit → 128 devices (commonly used)

10-bit → More addresses (rare)

## What is ACK and NACK?

ACK → Receiver pulls SDA LOW to confirm data received

NACK → Receiver does not acknowledge

## What is START condition?

SDA goes LOW while SCL is HIGH, indicating start of communication.

## What is STOP condition?

SDA goes HIGH while SCL is HIGH, ending communication.

## What happens if two masters start together?

Arbitration occurs; the master sending LOW wins, the other stops.

## What is clock stretching?

Slave holds SCL LOW to delay communication until ready.

## What are I²C speed modes?
| Mode       | Speed    |
| ---------- | -------- |
| Standard   | 100 kbps |
| Fast       | 400 kbps |
| Fast+      | 1 Mbps   |
| High-Speed | 3.4 Mbps |


## What if slave does not send ACK?

Master assumes device not present or error occurred.

## Can slave initiate communication?

❌ No. Only master can start communication.

## Why is I²C slower than SPI?

Because:

Addressing overhead

ACK/NACK bits

Only 2 wires

## 7-bit vs 10-bit addressing?

7-bit → 128 devices (commonly used)

10-bit → More addresses (rare)

## What is ACK and NACK?

ACK → Receiver pulls SDA LOW to confirm data received

NACK → Receiver does not acknowledge

## What happens if two masters start together?

Arbitration occurs; the master sending LOW wins, the other stops.

## What is clock stretching?

Slave holds SCL LOW to delay communication until ready.

## What are I²C speed modes?

| Mode       | Speed    |
| ---------- | -------- |
| Standard   | 100 kbps |
| Fast       | 400 kbps |
| Fast+      | 1 Mbps   |
| High-Speed | 3.4 Mbps |

## What if slave does not send ACK?

Master assumes device not present or error occurred.

## Can slave initiate communication?

❌ No. Only master can start communication.

## Why is I²C slower than SPI?

Because:

Addressing overhead

ACK/NACK bits

Only 2 wires

## What is repeated START?

START condition without STOP, used when switching between read/write.

## What is bus arbitration?

Process that decides which master controls the bus in multi-master I²C.

## What is open-drain and why used?

Open-drain allows devices to only pull LOW, preventing bus conflict.

## What if SDA is stuck LOW?

Bus becomes busy, communication fails.

## How to detect I²C errors?

Missing ACK

Bus busy

Timeout

SDA/SCL stuck

## ACK vs NACK in read operation?

ACK → More data needed

NACK → Last byte received

## How does arbitration work?

Master monitoring SDA:

     - LOW wins

     - HIGH loses and stops transmitting

## What are reserved addresses?

Addresses used for:

     - General call

     - Future use

     - Special commands

## Why SDA changes only when SCL is LOW?

To avoid false START/STOP detection.

## What is R/W bit?

Indicates:

   - 0 → Write

   - 1 → Read

## How to choose pull-up resistor?

Depends on:

       - Bus speed

       - Capacitance

       - Devices count
        (Common value: 4.7 kΩ)

## I²C vs SPI?
| Feature    | I²C    | SPI  |
| ---------- | ------ | ---- |
| Wires      | 2      | 4    |
| Speed      | Medium | High |
| Addressing | Yes    | No   |
| Complexity | Medium | Low  |

## Two slaves same address?

Use:

- Address pins

- I²C multiplexer


## How many devices on one bus?

Theoretically 127, practically limited by capacitance.

## Real-time use?

Sensors, RTCs, EEPROMs, displays.

## How ESP32 implements I²C?

Using hardware I²C controller with configurable SDA/SCL pins.

## ACK missing mid-transfer?

Master stops communication.

## Why repeated START?

To avoid releasing the bus.

## Long-distance communication?

❌ No, due to capacitance and noise.

## Common problems?

- Missing pull-ups

- Wrong address

- Clock speed mismatch

- Noise


# SPI


## 1️⃣ What is SPI?
SPI (Serial Peripheral Interface) is a synchronous, serial communication protocol used for high-speed data transfer between a master and one or more slave devices.

Commonly used in microcontrollers, SoCs, sensors, ADCs, DACs, displays, flash memory, SD cards, etc.

## 2️⃣ Why SPI is called Synchronous?
 
Because data transfer happens using a clock signal.

  - The master generates the clock

  - Both master and slave use this clock to send and receive data at the same time


## 3️⃣ SPI Architecture (Who controls whom?)
🔹 Master–Slave Architecture

- Master

  - Generates clock

  - Selects slave

  - Starts and stops communication

- Slave

  - Responds to master

  - Sends/receives data only when selected
 
  There is always at least one master

  ## 4️⃣ SPI Signals / Pins

  | Signal         | Full Form                  | Direction      | Meaning             |
| -------------- | -------------------------- | -------------- | ------------------- |
| **MOSI**       | Master Out Slave In        | Master → Slave | Data sent by master |
| **MISO**       | Master In Slave Out        | Slave → Master | Data sent by slave  |
| **SCLK / SCK** | Serial Clock               | Master → Slave | Clock signal        |
| **SS / CS**    | Slave Select / Chip Select | Master → Slave | Selects the slave   |

## 5️⃣ Basic SPI Communication Flow

1️⃣ Master pulls CS LOW (selects slave)

2️⃣ Master generates clock pulses (SCLK)

3️⃣ Data shifts:

    - Master sends bits on MOSI

    - Slave sends bits on MISO

4️⃣ After data transfer → CS goes HIGH

5️⃣ Communication ends

- 🟢 Data transfer is FULL-DUPLEX

Send + Receive happens simultaneously


##  6️⃣ SPI Data Transfer (Shift Registers Concept)

SPI uses shift registers internally.

Example (8-bit transfer):

  - On every clock pulse:

     - 1 bit is shifted out from master

     - 1 bit is shifted in from slave

So after 8 clock pulses:

     - 8 bits transmitted

     - 8 bits received

This is why SPI is faster than I²C and UART

## 7️⃣ Clock Polarity (CPOL) & Clock Phase (CPHA)

🔹 CPOL – Clock Polarity

Defines idle state of clock

    - CPOL = 0 → Clock idle LOW

    - CPOL = 1 → Clock idle HIGH

🔹 CPHA – Clock Phase

Defines when data is sampled

    - CPHA = 0 → Data sampled on first clock edge

    - CPHA = 1 → Data sampled on second clock edge

SPI Modes (0 to 3)

| Mode   | CPOL | CPHA |
| ------ | ---- | ---- |
| Mode 0 | 0    | 0    |
| Mode 1 | 0    | 1    |
| Mode 2 | 1    | 0    |
| Mode 3 | 1    | 1    |

Master and Slave must use the SAME mode, otherwise data corruption occurs.

## 8️⃣ SPI Timing Example

Mode 0 example:

   - Clock idle LOW

   - Data is sampled on rising edge

   - Data changes on falling edge

This ensures stable data during sampling

## 9️⃣ SPI with Multiple Slaves

There are two approaches:

🔹 1) Separate CS lines (Most common)

   - MOSI, MISO, SCLK shared

   - Each slave has separate CS

✅ Simple

❌ More GPIOs needed

🔹 2) Daisy Chain

   - Slaves connected in series
   
   - Data passes through each slave

✅ Fewer CS lines

❌ Complex, slower
🔟 SPI Speed

- SPI is very fast

- Speed depends on:

   - MCU clock
   
   - Peripheral capability
 
Typical speeds:

   - 1 MHz to 50+ MHz

📌 Faster than:

    - UART ❌

    - I²C ❌

## 1️⃣1️⃣ Advantages of SPI
✅ High speed

✅ Full-duplex communication

✅ Simple hardware

✅ No addressing overhead

✅ Flexible data size

## 1️⃣2️⃣ Disadvantages of SPI

❌ More pins required

❌ No built-in acknowledgment

❌ No error detection

❌ Short-distance communication

❌ Not standardized like I²C


## 1️⃣3️⃣ SPI vs I²C vs UART (Quick Comparison)

| Feature    | SPI       | I²C    | UART |
| ---------- | --------- | ------ | ---- |
| Clock      | Yes       | Yes    | No   |
| Speed      | Very High | Medium | Low  |
| Duplex     | Full      | Half   | Full |
| Pins       | 4+        | 2      | 2    |
| Addressing | No        | Yes    | No   |


