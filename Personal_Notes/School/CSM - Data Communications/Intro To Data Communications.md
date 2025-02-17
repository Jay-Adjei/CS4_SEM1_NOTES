---
course:
  - CSM 477
tags: 
last topic: Data Storage Technology
next topic: Data Transfer in Digital Circuits
note to self: Pg. 55
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

## Key Points
- **Rule:** The maximum permissible transmission rate of  a message is directly proportional to signal power and inversely proportional to channel noise.
- **Aim:** Provide the highest possible transmission rate at the lowest possible power with the least possible noise.
- Bit serial transmission is normally just called serial transmission and is the chosen communications method in many computer peripherals.

## Summary

-