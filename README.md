# UART Protocol

This project implements a **Universal Asynchronous Receiver/Transmitter (UART)** in **Verilog HDL**, including a **baud rate generator, transmitter, receiver, and top-level integration** with testbenches.  
It demonstrates **asynchronous serial communication** with configurable baud rate, parity generation/checking, and error detection.

---

## 📘 Functionality

### Baud Rate Generator
Divides the system clock to generate **baud rate pulses** for both transmission and reception.  

**Features:**
- Generates `tx_br` for transmitter timing  
- Generates `rx_br` for receiver timing  
- Parameterized clock frequency and baud rate  

---

### UART Transmitter (TX)
Responsible for converting **parallel 8-bit data into serial data**.  

**Operation sequence:**
1. Idle state (line remains HIGH)  
2. Start bit transmission  
3. Send 8 data bits (LSB first)  
4. Parity bit generation  
5. Stop bit transmission  

**Outputs:**
- `tx_out` – Serial output line  
- `busy` – Transmission in progress  
- `done` – Transmission completed  

---

### UART Receiver (RX)
Receives serial data and reconstructs the original **8-bit parallel data**.  

**Operation sequence:**
1. Detect start bit  
2. Shift incoming serial bits  
3. Reconstruct 8-bit data  
4. Perform parity check  
5. Validate stop bit  

**Outputs:**
- `rx_out` – Received 8-bit data  
- `done` – Reception complete  
- `busy` – Receiver active  
- `error` – Parity or stop bit error detected  

---

### Top Module
The **top module (`uart_top`)** integrates:
- Baud Rate Generator  
- UART Transmitter  
- UART Receiver  

The transmitter output is connected to the receiver input to perform **loopback communication testing**.

Code

---

## ⚙️ UART Frame Format
| Start | Data (8 bits) | Parity | Stop |
|   0   |   D0 - D7     |   P    |  1   |

Code
- **Start Bit:** Indicates beginning of transmission  
- **Data Bits:** 8-bit data transmitted LSB first  
- **Parity Bit:** Used for error detection  
- **Stop Bit:** Marks the end of the frame  

---

## 🧪 Simulation
The design can be simulated using:
- Vivado Simulator  
```
rx_data:00000000, rx_data:xxxxxxxx, tx_done:x, rx_done:x, tx_busy:x, rx_busy:x
rx_data:10110011, rx_data:xxxxxxxx, tx_done:0, rx_done:0, tx_busy:0, rx_busy:0
rx_data:10110011, rx_data:xxxxxxxx, tx_done:0, rx_done:0, tx_busy:1, rx_busy:0
rx_data:10110011, rx_data:xxxxxxxx, tx_done:0, rx_done:0, tx_busy:1, rx_busy:1
rx_data:10110011, rx_data:xxxxxxxx, tx_done:1, rx_done:0, tx_busy:0, rx_busy:1
rx_data:10110011, rx_data:10110011, tx_done:0, rx_done:1, tx_busy:0, rx_busy:1
rx_data:11001010, rx_data:10110011, tx_done:0, rx_done:1, tx_busy:0, rx_busy:0
rx_data:11001010, rx_data:10110011, tx_done:0, rx_done:0, tx_busy:1, rx_busy:0
rx_data:11001010, rx_data:10110011, tx_done:0, rx_done:0, tx_busy:1, rx_busy:1
rx_data:11001010, rx_data:10110011, tx_done:1, rx_done:0, tx_busy:0, rx_busy:1
rx_data:11001010, rx_data:11001010, tx_done:0, rx_done:1, tx_busy:0, rx_busy:1
```

---
**Testbenches provided verify:**
- Baud rate generation  
- UART transmission  
- UART reception  
- End-to-end loopback communication  

---

## 🚀 Applications
- FPGA serial communication  
- Embedded systems communication  
- Digital communication learning  
- Verilog RTL design practice  

---
