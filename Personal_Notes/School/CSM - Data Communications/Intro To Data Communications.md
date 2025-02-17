---
course:
  - CSM 477
tags: 
last topic: Transmission Media
next topic: Transmission Media
note to self: 
status: Incomplete
---

2025-02-09 20:25

# Intro To Data Communications

## Detailed Notes
### **Data Communications**
This concerns the transmission of digital messages to devices external to the message source.
**External Devices:** independently powered circuitry that exists beyond the chassis of a computer or other digital message source. 

### **Communications Channel**
A pathway over which information can be conveyed.
-Information is represented by individual data bits.
-The message source is the transmitter, and the destination id the receiver.
#### **Channel Types:**
- Simplex Channel: A channel whose direction is unchanging. Eg. Radio channel.
- Half-Duplex Channel: A single physical channel in which the signal may be reversed. Messages flow in two directions, but never at the same time. Eg. phone call, also used by centronics.
- Full-Duplex Channel: allows simultaneous message exchange in both directions. It consists of 2 simplex channels. The transmission rate of the reverse channel may be slower if it used only for flow control of the forward channel.

### **Serial Communications**
- Bit serial transmission conveys a message one bit at a time through a channel.
- Byte serial transmission conveys 8 bits at a time through 8 parallel channels. (Centronics printer interface is a case where byte-serial transmission is used.)
- **Examples:** 16 bit wide data bus to transfer data between a microprocessor and memory chips, when communicating with a timesharing system over a modem, only a single channel is available, and bit-serial transmission is required.

### **Transmission Media**
- The simplest transmission media consists of a pair of conductors.
- Inter-equipment communication often uses flat ribbon cables with multiple lines and a common return wire.
- These cables are highly prone to noise from nearby lines due to inductive or capacitive interference.
- Twisted pairs of wires improve noise immunity.
- Analog signals require amplifiers every 5–6 km to maintain signal strength.

### **Baud Rate**
- Refers to the signaling rate at which data is sent through a channel and is measured through electrical transitions per second.
	Simply put, Number of **signal changes (symbols) per second**
- In **EIA232**, baud rate = bit rate.
- **9600 baud** = **9600 bits/sec**, each bit lasts **104 microseconds**(1/9600)

### **Channel Efficiency**
- **Channel efficiency** is the ratio of useful data transmitted per second.
- If **2 transitions per bit**(like in non-return-to-zero coding) are needed, **9600 baud** gives **4800 bps**.
- It excludes framing, formatting, and error-checking bits, making efficiency **less than 1**.

### **Data Rate**
- **Data rate** ([[bit rate]]) measures bits transmitted per second, often mistaken for baud rate.
- **Bandwidth** determines channel capacity.
- **Max data rate** depends on bandwidth(directly proportional) and noise(inversely proportional) level.
- **Protocols** define message structure, framing, error detection, and transmission rules.
- A communication protocol is an agreed upon convention that  defines the order and meaning of bits in a serial transmission.
- **Protocol design** determines channel efficiency, not hardware.
- There is a **tradeoff** between efficiency and reliability—adding error detection improves noise immunity but reduces efficiency.

### **Asynchronous vs. Synchronous**
#### **Asynchronous Transmission**

- Data is sent in **small bursts** instead of a continuous stream.
- Each packet has **start and stop bits** to signal when transmission begins and ends.
- There are **variable pauses** between packets, meaning data is not sent at a uniform rate.
- Since there's no external clock, the receiver must **rely on start/stop bits** to recognize data.
- **Pros:** Simple and low-cost, works well for small amounts of data.
- **Cons:** Less efficient due to added start/stop bits and potential timing mismatches.

#### **2. Synchronous Transmission**

- Data is sent **continuously** in a steady stream, synchronized with a **clock signal**.
- A **separate timing channel** transmits clock pulses, telling the receiver when to read each bit.
- The receiver **"[[latches]]"** onto each clock pulse, ensuring data is read at the correct time.
- Since the clock controls timing, **no start/stop bits are needed**, making transmission more efficient.
- **Pros:** Faster and more reliable, ideal for large data transfers.
- **Cons:** More complex and requires additional hardware for clock synchronization.

#### **3. Key Difference**

- **Asynchronous** = No clock, uses start/stop bits, works best for small, sporadic data transfers.
- **Synchronous** = Uses a clock, sends continuous data, best for fast and accurate transmission.

#### **Final Takeaway:**

- If **timing accuracy and speed** are priorities, **synchronous** transmission is better.
- If **simplicity and flexibility** are needed, **asynchronous** transmission works well.

### **Manchester Coding**
#### **1. Manchester Coding**

- A **self-timed** encoding method for converting data into an electrical waveform.
- Two common types: **[[Non-Return-to-Zero (NRZ)]] & [[Biphase Manchester Coding]]**.
- Ensures synchronization without a separate clock signal.

#### **2. Asynchronous Systems**

- No separate **timing channel** is used.
- **Transmitter & receiver must agree on a baud rate** beforehand.
- The receiver uses a **local oscillator** to generate a matching clock signal.
- Data is sent in **small packets (10 or 11 bits)**, with 8 bits for actual information.
- When idle, the **signal remains at logic '1'**.

#### **Key Takeaway:**

- **Manchester coding** helps keep data synchronized within a single signal.
- **Asynchronous systems** rely on pre-set baud rates and local oscillators instead of a separate timing channel.

### **Data Packet**
#### **Data Packet Structure**

- Each **[[data packet]]** starts with a **logic '0' (Start Bit)** to signal the receiver.
- The **start bit** triggers the receiver’s **internal clock oscillator**.
- **8 data bits** are transmitted **bit by bit** at the set **baud rate**.
- The packet ends with a **parity bit (for error detection) and a stop bit**.

#### **2. Purpose of Short Packet Length in Asynchronous Systems**

- Short packets prevent **timing drift** between the sender and receiver.
- **High-quality oscillators**(such crystal oscillators) keep synchronization stable over **11-bit periods**.
- Each **new start bit resets synchronization**, allowing **flexible pauses between packets**.

#### **3. [[EIA232]] Standard & Serial Communication**

- The **EIA232 standard** defines **electrical, timing, and mechanical** aspects of serial communication.
- It **does not include** the asynchronous serial protocol used in the given example.

#### **Key Takeaway:**

- Asynchronous transmission relies on **start and stop bits** for synchronization.
- **Short packets prevent timing errors** in systems with separate oscillators.
- The **EIA232 standard** governs hardware but not specific asynchronous protocols.

## Key Points
- **Rule:** The maximum permissible transmission rate of  a message is directly proportional to signal power and inversely proportional to channel noise.
- **Aim:** Provide the highest possible transmission rate at the lowest possible power with the least possible noise.
- Bit serial transmission is normally just called serial transmission and is the chosen communications method in many computer peripherals.

## Summary

-