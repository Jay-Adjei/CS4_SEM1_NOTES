---
course:
  - CSM 477
tags: 
last topic: Optical Fibre
next topic: Radio Transmission
note to self: Try and cover the radio and satelite transmissions
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

- Short packets prevent **[[timing drift]]** between the sender and receiver.
- **High-quality oscillators**(such crystal oscillators) keep synchronization stable over **11-bit periods**.
- Each **new start bit resets synchronization**, allowing **flexible pauses between packets**.

#### **3. [[EIA232]] Standard & Serial Communication**

- The **EIA232 standard** defines **electrical, timing, and mechanical** aspects of serial communication.
- It **does not include** the asynchronous serial protocol used in the given example.

#### **Key Takeaway:**

- Asynchronous transmission relies on **start and stop bits** for synchronization.
- **Short packets prevent timing errors** in systems with separate oscillators.
- The **EIA232 standard** governs hardware but not specific asynchronous protocols.

### **Parity and checksums**
#### **What is a Parity Bit?**

- A **parity bit** is an **extra bit added to a binary data transmission** for **error detection**.
- It helps check if the number of `1`s in the data is **even or odd**.
- Used in **serial communication, memory storage, and networking** to detect errors.

#### **2. Types of Parity:**

- **[[Even Parity]]:** Ensures the **total number of 1s** (including the parity bit) is **even**.
- **[[Odd Parity]]:** Ensures the **total number of 1s** (including the parity bit) is **odd**.

#### **3. How Parity Works:**

- **Sender calculates the parity bit** based on the data and appends it.
- **Receiver recalculates parity** upon arrival and compares it with the received parity bit.
- If the parity doesn’t match, **an error is detected**.

#### **Steps to Calculate Even and Odd Parity**

##### **General Rules:**

1. **Count the number of 1s** in the data bits.
2. **For Even Parity** → Add a parity bit to make the total **even**.
3. **For Odd Parity** → Add a parity bit to make the total **odd**.
4. **Attach the parity bit** at the end of the data.

#### **4. Other Types of Parity:**

- **None (No parity bit used)** – The system does not generate or check a parity bit.
- **Space Parity:** Parity bit is always **0** (used as a filler).
- **Mark Parity:** Parity bit is always **1** (also used as a filler).

#### **5. Parity Check Limitations:**

- **Detects single-bit errors** but **cannot fix errors**.
- **Fails if an even number of bits are flipped** (e.g., `1010` → `1001` still has the same parity).
- Works best in **small packet sizes**.

#### **Final Takeaway:**

- **Parity bits** provide a **simple way to detect errors** in communication.
- **Even/Odd parity** ensures that data integrity is maintained in basic transmission.
- **Limitations:** Parity cannot fix errors and fails if multiple bits change.

#### **Checksum**
#### **What is a Checksum?**

- A **checksum** is a calculated **numeric value added to data packets** for **error detection**.
- It is computed by **arithmetically adding** the values of all data packets.
- The checksum ensures that the **sum of data + checksum = 0** for accurate transmission.

---

#### **2. How Checksum Works:**

1. **Sender Side:**
    
    - Computes the **checksum value** by adding packet data.
    - Appends the **checksum to the transmitted packet**.
2. **Receiver Side:**
    
    - Recomputes the **sum of received data + checksum**.
    - If the sum is **zero**, the data is assumed **correct**.
    - If the sum is **nonzero**, an **error is detected**.

---

#### **3. Checksum Advantages:**

✔ **Detects errors in data transmission.**  
✔ **Simple mathematical operation** (fast computation).  
✔ Used in **networking (TCP/IP, UDP), storage (RAID), and file integrity checks**.

---

#### **4. Error Correction (Beyond Detection)**

- Errors **can be corrected** if additional **error-correcting codes (ECC)** are added.
- This is useful when:
    - **Retransmission is not possible** (e.g., deep-space communication).
    - The **error probability is high** (e.g., noisy channels).
- **Downside:** Error correction **reduces channel efficiency** by increasing overhead, and there is noticeable drop in [[channel throughput]].

#### **Steps**
| **Step**   | **Action**                                                                    |
| ---------- | ----------------------------------------------------------------------------- |
| **Step 1** | Divide data into fixed-size blocks (e.g., 8-bit).                             |
| **Step 2** | Add all blocks together using **binary addition**.                            |
| **Step 3** | If sum exceeds block size, **truncate it**.                                   |
| **Step 4** | Compute **one’s complement** of the sum (flip first 6 bits).                  |
| **Step 5** | **Send data + checksum** to the receiver.                                     |
| **Step 6** | Receiver **adds received data + checksum** and checks if the sum is **zero**. |
| **Step 7** | If the sum is NOT zero, **error detected** → Request retransmission.          |

### **Data Compression**
#### **What is Data Compression?**

- Data compression **reduces the size of data** for transmission or storage.
- It assigns **shorter codes to frequently used characters** and **longer codes to rarely used ones**.

---

#### **2. Benefits of Compression**

✔ **Reduces the total data sent** without losing information.  
✔ **Faster transmission times** and lower storage requirements.  
✔ **Up to 50% or more savings** in data size.

---

#### **3. Types of Data Compression**

- **Text Compression:** Assigns **shorter binary codes** to common characters.
- **Image Compression:** Reduces repetitive patterns (e.g., **Run-Length Encoding, JPEG**).
- **Program Compression:** Software and executables typically **compress less (15-20%)** than images.

---

#### **4. Huffman Coding (Example of Lossless Compression)**

- Used in **fax transmission, data communications, and file compression**.
- Works by **assigning short codes** to common symbols and **longer codes** to rare ones.
- Example: Instead of **sending each white pixel separately**, **one code** represents **1000 white pixels** in a row.

---

#### **5. When Compression is Less Effective**

- If data is already random (e.g., **randomly distributed black ink on white paper**), compression **won’t work well**.
- Best used where **patterns and repetition exist**.

---

### **Final Takeaway:**

- **Data compression saves bandwidth and storage**.
- **Huffman coding** is widely used for efficient encoding.
- **Compression efficiency depends on data type** (e.g., images compress better than programs)

### **Data Encryption**
#### **What is Data Encryption?**

- **Encryption** secures communication by **scrambling data** into an unreadable format.
- Only **authorized receivers** can decode and restore the original message.

---

#### **2. Why is Encryption Important?**

✔ **Prevents unauthorized access** (protects privacy).  
✔ **Secures digitized conversations** (e.g., phone calls, emails, fax).  
✔ **Protects data from interception** over networks.

---

#### **3. How Encryption Works**

1. **Data is converted into an unreadable format (ciphertext).**
2. **Only devices with the correct decryption key can restore the message.**
3. **Unauthorized interception results in scrambled, unreadable data.**

---

#### **4. Implementation of Encryption**

- **Built-in circuits** in communication devices perform encryption automatically.
- **[[External circuits]]** allow portable encryption/decryption.
- **Encryption can be hardware-based or software-based** depending on the system.

---

### **Final Takeaways**

- **Encryption ensures secure communication** in data transmission.
- **Only authorized users can decrypt messages.**
- **Used in banking, military, email security, and secure messaging apps.**

Details on data encryption -> [[In depth data encryption]]

### **Data Storage Technique**
#### **Relationship Between Communication and Storage**

- **Communication technology** is usually associated with **real-time data exchange** between distant devices.
- However, **many communication techniques** (like error correction and signal processing) are also **used in data storage** to ensure accurate data retrieval.

---

#### **2. Error Correction in Data Storage**

- **Error-correcting codes (ECC)** used in communication (to handle noise) are also used in **data storage**.
- These techniques **detect and correct errors** when reading digital data from storage media.

---

#### **3. Applications of Error Correction in Storage**

✅ **Compact Discs (CDs) & CD-ROMs:**

- Use **Reed-Solomon Error Correction (RS ECC)** to correct data errors from scratches or dust.  
    ✅ **Hard Drives (HDDs) & Solid-State Drives (SSDs):**
- Use **ECC algorithms** to ensure correct data retrieval.  
    ✅ **Tape Backup Systems:**
- Store large amounts of data and use **error-correcting codes** to ensure long-term accuracy.

---

### **Final Takeaways**

✔ **Data communication and data storage share similar error-handling techniques.**  
✔ **Error correction ensures reliable data retrieval from storage media.**  
✔ **CDs, hard drives, and tape backups all use ECC to prevent data loss.**

### **Data Transfer in Digital Circuits**
#### **How Data is Transferred in Digital Circuits**

- Data is grouped into **packets of 8, 16, or 32 bits** and stored in **registers** (temporary holding units).
- Each **bit in a register** is transferred in **parallel** through separate conductors.

---

#### **2. Role of Buses in Data Transfer**

- A **bus** is a channel of **parallel wires** that connects different registers.
- The **source register** sends data through **output conductors** to the bus.
- The **destination register** receives data via **input conductors**.

---

#### **3. Behavior of Registers During Data Transfer**

- After transmission, the **destination register contains the same data as the source register**.
- The **source register is not erased** after transfer.

---

#### **4. Controlling Data Flow with Switches**

- **Transmit switches** allow data from the source register to enter the bus.
- **Receive switches** allow data to be captured by the destination register.
- A **central control unit** manages these switches to avoid conflicts.

---

#### **5. Bus Contention & Conflict Prevention**

- **Bus contention** occurs when **multiple sources attempt to transmit simultaneously**, causing electrical conflicts.
- **If not controlled, contention can cause data loss or damage circuitry**.
- To prevent contention:
    - Only **one source register** transmits at a time.
    - A **central control unit** ensures orderly data flow.

---

#### **6. Microprocessor Bus Characteristics**

- Data buses in a **microprocessor** are **half-duplex** (data flows in one direction at a time).
- **Proper circuit design** prevents bus contention.

---

#### **Final Takeaways**

✔ **Data transfer between registers occurs through buses using switches.**  
✔ **A central control unit ensures only one source transmits at a time.**  
✔ **Bus contention can cause conflicts and must be prevented.**  
✔ **Microprocessors use half-duplex buses for controlled data flow.**

#### **Transmission Over Short Distances**
##### **Data Transmission Within an Integrated Circuit (IC)**

- When **source and destination registers** are within the **same microprocessor chip**, data transfer occurs over **very short distances** (thousandths of an inch).
- **Advantages of short-distance transmission:**
    - **Low power signals** are sufficient.
    - **Minimal delay** since data travels a very short distance.
    - **Less noise and distortion**, ensuring accurate transmission.

---

##### **2. Limitations of a Single Chip**

- Although **integrating all computing functions on one chip** would be ideal, it’s **not yet possible** to fit the CPU, memory, disk controllers, display drivers, etc., on a single IC.

---

##### **3. Data Transmission Between ICs ("Off-Chip" Communication)**

- When data moves **outside the chip**, signals must be **amplified** to maintain strength.
- **Conductors extend out of the chip** through **external pins**, allowing communication with other ICs.

---

##### **4. Bus Transmission Over Circuit Boards**

- Signals from microprocessor chips can travel up to **one foot on a printed circuit board (PCB)**.
- If more devices are connected, **signal strength weakens**.
- **Buffer circuits** can **boost signal strength** for longer distances or multiple connections (e.g., memory chips).

---

##### **Final Takeaways**

✔ **Short-distance communication within an IC is efficient due to minimal power use and noise.**  
✔ **Longer-distance data transfer (between ICs) requires amplification and external connectors.**  
✔ **Bus signals on PCBs may need buffer circuits for extended transmission.**

#### **Noise and Electrical Distortion**
##### **Why Noise and Distortion Occur**

- **High switching rates** and **low signal strength** in data, address, and control buses make them **prone to noise**.
- Extending buses **beyond circuit boards** can create **serious issues** due to external interference.

---

##### **2. How Conductors Pick Up Noise**

- Long conductors in **printed circuit boards (PCBs) or cables** can act as **antennas**, picking up noise from:
    
    - **Motors**
    - **Switches**
    - **Electronic circuits**
- This **induces unwanted currents** in the signal conductors.
    

---

##### **3. Impact of Noise on Digital Circuits**

- Noise can **increase error rates** as conductor lengths increase.
- A **single bit error** in an instruction code (e.g., from memory to a microprocessor) can introduce **invalid instructions**, causing system failures.

---

##### **4. Electrical Signal Distortion**

- Signals can **change shape** as they travel through metallic conductors.
    
- A **clean rectangular pulse** may arrive as a **rounded or distorted waveform** due to:
    
    - **Capacitance effects**
    - **Inductance in copper cables**
    - **Long transmission distances**
- This leads to **ringing effects** at the rising and falling edges of pulses.
    

---

##### **5. Solutions to Noise and Distortion**

1. **Increase Signal Power** → Helps signals remain strong over long distances.
2. **Reduce Transmission Rate** → Slower switching reduces distortion.
3. **Use Special Amplifier Circuits** → Amplifiers **boost** weak signals.
4. **Use Noise Margins** → Ensure voltage levels remain within valid logic '1' and '0' thresholds.

---

##### **6. Role of Noise Margin**

- **[[Noise margin]]** is the difference between:
    
    - **Actual signal voltage**
    - **Minimum required voltage for logic 1 or 0**(threshold voltage)
- **A higher noise margin means better noise immunity.**
    

---

##### **Final Takeaways**

✔ **Conductors can pick up external noise, causing bit errors.**  
✔ **Long cables distort signals, reducing accuracy.**  
✔ **Amplifiers and noise margins help maintain signal integrity.**  
✔ **Reducing transmission speed improves reliability over long distances.**

#### **Transmission Over Medium Distances**
##### **Why Medium-Distance Transmission is Needed**

- Peripherals like **printers and scanners** cannot be placed inside a computer.
- Using **long internal buses** to connect them introduces **noise and distortion**.
- A better solution is **a bus interface circuit** that allows reliable communication.

---

##### **2. How Data is Transmitted to Peripherals**

- A **bus interface circuit** is installed in the computer.
- The interface includes:
    - **A holding register** for peripheral data.
    - **Timing and formatting circuitry** to organize data.
    - **Signal amplifiers** to strengthen transmission.

---

##### **3. Steps in Data Transmission**

1. The **microprocessor stores data** in the holding register.
2. Data is **formatted and sent with error-detecting codes**.
3. Signal power is **boosted before transmission** through the cable.
4. These steps **prevent noise and distortion** from corrupting the data.

---

##### **4. Preventing Noise Exposure**

- Only **necessary data** is sent to the peripheral.
- This reduces **unwanted party-line transactions** on the internal bus.
- Data can be sent in:
    - **Byte-serial format** (multiple channels).
    - **Bit-serial format** (single channel).

---

##### **5. Importance of Transmission Medium**

- Data transmission depends on **medium characteristics**:
    - **Metallic conductors** (cables).
    - **Fiber optics** (light beams for high-speed data).
    - **Wireless transmission** (electromagnetic waves).

---

##### **6. Signal Boosting Methods**

- **Amplifiers** enhance analogue signals for long-distance transmission.
- **Repeaters** are used for digital signals every **2-3 km** to restore data integrity.

---

##### **Final Takeaways**

✔ **Internal buses are not suitable for long peripheral connections.**  
✔ **Bus interface circuits format, amplify, and transmit data efficiently.**  
✔ **Byte-serial and bit-serial formats enable flexible data transfer.**  
✔ **Amplifiers and repeaters help maintain signal strength over distances.**

### **Cabling**
#### **Twisted Pair Cabling Basics**

- Consists of **two wires twisted together** in pairs.
- Each pair includes:
    - **+ve (positive) data signal**
    - **-ve (negative) data signal**
- Twisting the wires **reduces noise interference**.

---

#### **2. How Twisted Pairs Reduce Noise**

- Any noise affecting one wire also **affects the other**.
- Since the wires are **180° out of phase**, noise **cancels out** at the receiver.
- Best used in systems with **balanced transmission**.

---

#### **3. Types of Twisted Pair Cables**

- **Unshielded Twisted Pair (UTP)**
    
    - **No shielding**, making it cheaper but more prone to interference.
    - Used in **Ethernet (10BaseT) and Token Ring networks**.
    - **Uses RJ45, RJ11 connectors**.
    - **Typical impedance: 100 ohms**.
- **Shielded Twisted Pair (STP)**
    
    - Has an **extra shielding layer** for better noise rejection.
    - Common in **IBM Cabling Systems (ICS)**.

---

#### **4. Enhancing Noise Reduction**

- **More twists per foot** = **Better noise cancellation**.
- **Adding a shielding layer** further reduces interference.

---

#### **5. Other Cable Types**

- **Coaxial Cable**
    - Two conductors with an insulating layer between them.
    - **Better shielding against external interference**.
- **Optical Fiber**
    - **Uses light signals** for data transmission.
    - **Core** (refracts light), **Cladding** (reflects light), and **Jacket** (protection).
    - Based on **total internal reflection (TIR)** to prevent signal loss.

---

#### **6. Light Behavior in Different Media**

- **Light moves differently through materials (air, water, glass, etc.)**.
- **Small angles of incidence → Reflection**.
- **Large angles of incidence → Refraction (bending)**.
- **Objects underwater appear displaced** due to refraction.

---

#### **7. Optical Fiber Transmission Principles**

- **Uses light instead of electrical signals**.
- **Total internal reflection (TIR)** keeps light within the fiber.
- **Core refracts light, cladding reflects it back** to minimize loss.

---

#### **8. Optical Fiber Transmission Modes**

- **Step Index Mode**
    
    - Large core, multiple reflections off the cladding.
    - Causes **signal distortion** due to different light travel times.
- **Graded Index Mode**
    
    - Gradual refractive index change bends light **back to the core**.
    - Reduces signal distortion for better reception.
- **Single Mode**
    
    - Very thin core (**9 microns**).
    - **Light travels in a straight line**, minimizing distortion.
    - **Best for long-distance transmission**, uses **laser sources**.

---

#### **9. Optical Fiber Specifications**

- **Indoor Cables**
    
    - **LED light sources**.
    - **Multimode transmission (~850nm wavelength)**.
    - **Signal loss: 3.5 dB/km**.
- **Outdoor Cables**
    
    - **Laser sources**.
    - **Single-mode transmission (~1170nm wavelength)**.
    - **Signal loss: 1 dB/km**.

---

#### **10. Advantages of Optical Fiber**

✔ **High bandwidth** → Supports large data transmission.  
✔ **Low signal loss** → Can transmit over long distances.  
✔ **Immune to EMI/RFI** → No electromagnetic interference.  
✔ **Highly secure** → Hard to tap into fiber optics.  
✔ **Lightweight and compact** → Easier installation.

---

#### **11. Disadvantages of Optical Fiber**

❌ **Fragile** → Susceptible to bending or vibration damage.  
❌ **Difficult to splice** → Requires specialized tools.  
❌ **High initial cost** → More expensive than copper for low-speed applications.

---

#### **12. Unguided Transmission Media**

- **Transmits data through the air instead of cables**.
- **Not bound to physical pathways**, classified by **wave propagation**.

---

#### **Final Takeaways**

✔ **Twisted pair cabling cancels out noise through phase shifting.**  
✔ **UTP is cheaper and common in Ethernet, while STP has better shielding.**  
✔ **More twists per foot improve noise rejection.**  
✔ **Coaxial cables offer better shielding, while optical fiber provides superior speed.**  
✔ **Light follows total internal reflection in optical fibers to prevent signal loss.**  
✔ **Three optical transmission modes: Step Index, Graded Index, and Single Mode.**  
✔ **Single-mode fiber is best for long-distance, high-speed communication.**  
✔ **Optical fibers are immune to EMI but fragile and costly.**  
✔ **Unguided transmission transmits data wirelessly through the air.**

## Key Points
- **Rule:** The maximum permissible transmission rate of  a message is directly proportional to signal power and inversely proportional to channel noise.
- **Aim:** Provide the highest possible transmission rate at the lowest possible power with the least possible noise.
- Bit serial transmission is normally just called serial transmission and is the chosen communications method in many computer peripherals.

## Summary

-