---
course:
  - CSM 477
tags: 
last topic: Optical Fibre
next topic: Radio Transmission
note to self: Try and cover the radio and satelite transmissions
status: Completed
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

### **Radio Transmission**

#### **Definition:**

- The transmission of data using radio waves in free space, often used for communication without physical cables.

#### **Function:**

- Used for line-of-sight microwave transmission.
- Provides an alternative where laying cables is difficult, such as linking buildings separated by roads.

#### **Advantages:**

- Supports high data rates over long distances, similar to coaxial cable systems.
- Utilized in long-haul telecommunications as an alternative to fiber optic or coaxial cables.

#### **Challenges:**

- Terrestrial radio links are affected by electrical and atmospheric interference.
- Unlike terrestrial links, satellite transmission avoids such disturbances as radio beams travel freely in space.

#### **Technical Aspects:**

- Uses parabolic dish antennas at UHF frequencies for high directionality.
- Directivity depends on dish diameter and wavelength, affecting signal gain.
- The range between two line-of-sight parabolic antennas is calculated as:  
    **d = 7.14 (kh)¹/² km**, where:
    - **h** = antenna height (km),
    - **k** = factor for Earth's curvature (≈1.33).

#### **Final Takeaways:**

✔ Radio transmission enables wireless communication without cables.  
✔ Microwave links support high-speed, long-distance data transfer.  
✔ Terrestrial radio links face interference, unlike satellite transmission.  
✔ Parabolic dish antennas ensure precise, high-directional transmission.

### **Satellite Communication** 

#### **Definition:**

**Satellite Communication:** A microwave relay system used for point-to-point and broadcast transmission via satellites.  
**RF Propagation:** The way radio waves travel through space, categorized into Ground Wave, Ionospheric, and Line-of-Sight (LOS).

---

#### **Function:**

**Satellite Communication:**

- Uplink frequency (1–10 GHz) transmits from Earth to satellite.
    
- Downlink retransmits to receiving stations.
    
- Ideal for broadcasting over wide areas.
    

**RF Propagation:**

- **Ground Wave:** Follows Earth's curvature (≤2 MHz).
    
- **Ionospheric:** Reflects off ionosphere (30–85 MHz); affected by time and weather.
    
- **Line-of-Sight (LOS):** Requires direct visual path; limited by Earth’s curve (used in FM, microwave, satellite).
    

---

#### **Transmission Path & Frequency:**

**Satellite Communication:**

- Uses higher frequencies, though above 10 GHz causes attenuation.
    
- High gain dish aerials required.
    

**RF Propagation:**

- Ground Wave: AM radio.
    
- Ionospheric: Double hop; reflects signals back to Earth.
    
- LOS: Used in FM, satellite; affected by curvature.
    

---

#### **Challenges:**

**Satellite Communication:**

- High launch cost and power requirements.
    
- Signal delay (240–300 ms).
    
- [[Doppler shift]] affects frequency.
    
- Signal distortion in telephone/digital communication.
    

**RF Propagation:**

- **Ground Wave:** Limited by frequency and terrain.
    
- **Ionospheric:** Variable based on ionosphere conditions.
    
- **LOS:** Limited range (up to 100 km), affected by obstacles and reflection.
    

---

#### **Example:**

**Satellite Communication:** Used for broadcast TV, internet via satellite, etc.  
**RF Propagation:**

- **Ground Wave:** AM radio
    
- **Ionospheric:** Long-distance HF radio
    
- **LOS:** FM radio, satellite, microwave links
    

---

### **Final Takeaways**

✔ Satellite communication acts like a microwave relay, using uplink and downlink signals.  
✔ RF propagation includes ground wave, ionospheric, and LOS methods, each with specific frequency ranges.  
✔ Satellite communication enables wide coverage but has higher costs and delays.  
✔ RF propagation is effective for specific ranges but is affected by geography and atmospheric conditions.  
✔ All methods play essential roles in long- and short-range communication systems.

---

## **Microwave Communication vs Satellite Communication**

### **Definition**:

**Microwave Communication:** A form of **line-of-sight** wireless transmission using high-frequency radio waves.  
**Satellite Communication:** Uses **geostationary or low Earth orbit (LEO) satellites** as relay stations to transmit and receive signals over long distances.

---

### **Frequency Range:**

**Microwave Communication:** Operates between **3 to 10 GHz**.  
**Satellite Communication:** Operates typically between **1 to 10 GHz**.

---

### **Signal Path:**

**Microwave Communication:**

- Requires direct visibility between transmitter and receiver.
    
- Curvature of Earth limits range (~50 km); uses **repeaters** to extend.
    

**Satellite Communication:**

- Signals are sent from ground (uplink) to satellite and then back (downlink).
    
- Covers very large areas due to satellite altitude (e.g., 36,000 km in geostationary orbit).
    

---

### **Components:**

**Microwave:**

- Transmitter, Receiver, and Repeater stations.
    

**Satellite:**

- **Uplink** (transmits data to satellite),
    
- **Downlink** (receives data from satellite),
    
- **Transponders** (relay signals on different frequencies),
    
- **Footprint** (area on Earth where signals can be received).
    

---

### **Advantages:**

**Microwave Communication:**  
✔ No land ownership between towers required.  
✔ High bandwidth; small antennas due to short wavelengths.  
✔ Low land cost for tower setup.

**Satellite Communication:**  
✔ Wide-area coverage.  
✔ Ideal for broadcasting, GPS, and global communication.  
✔ LEO satellites (like Iridium) reduce delay and power needs.

---

### **Disadvantages:**

**Microwave Communication:**  
✘ Signal blocked by solid objects (e.g., birds, buildings, fog).  
✘ Affected by reflection, diffraction, and atmospheric refraction.  
✘ Limited range without repeaters.

**Satellite Communication:**  
✘ Expensive to launch and maintain.  
✘ Signal delay due to distance (especially geostationary).  
✘ Frequency shift due to Doppler effect in LEO systems.

---

### **Examples:**

**Microwave:** Point-to-point communication, TV relays, mobile phone backhaul.  
**Satellite:** Satellite TV, GPS, satellite internet, Iridium telecom system.

---

### **Final Takeaways**

✔ **Microwave** is short-range, line-of-sight, high-frequency communication best for local hops.  
✔ **Satellite** offers long-range global communication with uplink/downlink paths.  
✔ Microwaves use **repeaters**, while satellites use **transponders** in orbit.  
✔ Both are key technologies for modern telecommunication networks.

---

## **Types of Transmission Impairments**

### 1. **Attenuation**

**Definition:** The gradual loss of signal strength over distance.  
**Cause:**

- In hardware: signal weakens logarithmically over distance (measured in decibels).
    
- In software or terrestrial systems: affected by atmospheric conditions and square of distance.  
    **Solution:**
    
- Use of **amplifiers** (for analog) or **repeaters** (for digital) to boost signal.  
    **Note:** Attenuation is frequency-dependent; different frequencies may attenuate at different rates.
    

---

### 2. **Distortion**

**Definition:** Changes in the signal form or shape.  
**Cause:**

- More severe in analog systems.
    
- Results from unequal delay in signal components (frequency/phase distortion).  
  
**Solution:**

- Use of **equalization techniques**, **filters**, and **loading coils**.
    **Problem:** May lead to **data loss**, especially in digital transmission.
    

---

### 3. **Delay Distortion**

**Definition:** Type of distortion caused by varying propagation speeds for different frequencies.  
**Effect:**

- Leads to **inter-symbol interference**, where signals of adjacent bits overlap.
    
- Serious in **high-speed data** communication.
    

---

### **4. Noise**

**Definition:**  
Unwanted or interfering electrical signals that distort or corrupt the intended data during transmission. Noise reduces the accuracy and reliability of communication.

#### **Types of Noise:**

1. **Thermal Noise (Johnson–Nyquist Noise):**
    

- Caused by the **random motion of electrons** in conductors due to temperature.
    
- Present in **all electronic devices** and transmission media.
    
- Has a **uniformly wide frequency spectrum** (also called white noise).
    
- Although it cannot be completely eliminated, its level is usually very **low** (e.g., ~100 dB selective to 1 mW in MHz range).
    
- **Impact:** Represents the **upper limit** of system performance but is generally negligible in most applications.
    

2. **Gaussian Noise:**
    

- Appears as a **background hiss**, especially in analog telephone networks (PSTN).
    
- Produced in systems that **include amplifiers**.
    
- Characterized by a **zero average (DC) value** and a **Gaussian amplitude distribution**.
    
- **Impact:** Randomly alters signals; when above threshold, it can **convert correct signals into incorrect ones**.
    

**3. Jitter Noise (Phase Jitter):**

- Caused by **short-term variations** or **departures in the timing** of signal pulses from their expected positions.
    
- Known as **phase jitter** when this time variation affects the signal's phase.
    
- Behaves like **phase shift noise**, additive to the original signal.
    
- **Sources:**
    
    - Mostly occurs during **digital regeneration** in repeaters spaced along the medium.
        
    - Often influenced by the **pattern** of the transmitted signal, called **pattern-dependent jitter**.
        
- **Measurement:**
    
    - Quantified using **r.m.s (root mean square)** value.
        
    - Depends on:
        
        - Number of repeaters (**N**),
            
        - Bandwidth (**B**),
            
        - Power density of jitter at each repeater (**P**).
            
    - Formula:
        
        ![[Pasted image 20250402045024.png]]
- **Impact:** Jitter accumulates as the signal passes through each repeater, increasing error rates in digital transmission.
    

4. **Impulse Noise:**
    

- Consists of **high amplitude**, **short-duration** bursts or spikes.
    
- Often caused by external sources like **ignition systems** (cars), **lightning**, or **switching** equipment.
    
- Can affect **many consecutive bits** and may **corrupt or destroy an entire transmission frame**.
    
- **Impact:** Frames must be **retransmitted**, adding delays and decreasing efficiency.
    

#### **Other Noise Sources:**

- **Intermodulation Noise:**
    
    - Occurs when signals of **different frequencies** mix in a **nonlinear component**, such as a **non-linear amplifier**.
        
    - The result is the generation of **additional frequencies**, which interfere with the original signals.
        
    - Common in shared media like carrier systems.
        
- **Crosstalk:**
    
    - Caused by **electrical coupling** between **adjacent conductors** (e.g., cables placed too close).
        
    - The signal from one line **“leaks”** into another, creating interference.
        
    - Common in **telephone lines**, twisted pair cables, and dense circuit boards.
    

---

### **Signal-to-Noise Ratio (SNR)**

**Definition:** Measure of signal quality compared to background noise.  
**Formula:**

![[Pasted image 20250402044550.png]]

**Importance:** Higher SNR → better quality & higher possible data rate.

---

### Final Takeaways

✔ **Attenuation** reduces signal strength with distance.  
✔ **Distortion** changes signal form, especially in analog systems.  
✔ **Delay distortion** affects pulse timing and causes data overlap.  
✔ **Noise** comes in various forms and can corrupt data.  
✔ Noise distorts or corrupts data signals and limits system performance.  
✔ **Thermal** and **Gaussian** noise are continuous and system-based.  
✔ **Impulse** and **jitter** are sudden and damaging in nature.  
✔ **Jitter noise**, especially in digital systems, increases with each repeater and depends on timing patterns.  
✔ **Intermodulation** and **crosstalk** are due to system design issues.  
✔ Understanding all types of noise is critical for designing effective error control, shielding, and transmission systems.
✔ **SNR** is key for evaluating transmission performance.  
✔ Repeaters, filters, and amplifiers help mitigate these issues.

---

## **Public Switched Telephone Network (PSTN)**

#### **Definition:**  
A global system of interconnected voice-oriented public telephone networks.

#### **Signal Handling:**

- Analog speech/data signals are transmitted in the **300–400 Hz** bandwidth up to the **local exchange**.
    
- At the exchange, **multiple channels are combined** for wideband transmission via **modulation**.
    

#### **Modulation Process:**

- Modifies a **carrier signal** using parameters of the **message signal**.
    
- Allows efficient use of bandwidth and sharing of frequencies among multiple users.
    

#### **Benefits of Modulation in PSTN:**

- Prevents multiple speech signals from overlapping in the **same frequency range**.
    
- Enables **long-distance** and **multi-channel** communication over a single channel.
    

#### **Modulation Techniques Used:**

- **[[Amplitude Modulation (AM)]]**
    
- **[[Frequency Modulation (FM)]]**
    
- **[[Phase Modulation (PM)]]**
    
- **[[Pulse Code Modulation (PCM)]]**
    
- **[[Multiplexing]]**
    

---

### **Modem Categories**

#### **Function:**  
Converts **digital data** to **analog signals** (modulation) and vice versa (demodulation) for PSTN transmission.

#### **Speed Categories & Techniques:**

1. **Low-Speed (≤300 bps):**
    
    - Uses **Frequency Shift Keying (FSK)**
        
2. **Medium-Speed (≤1200 bps):**
    
    - Uses **Differentiated Phase Shift Keying (DPSK)**
        
3. **High-Speed (≥2400 bps):**
    
    - Uses **Quadrature Amplitude Modulation (QAM)**
        

---

### **Data Ratios**

#### **Telephone System Data Rates:**

- Follows pattern: **75 × 2ⁿ**
    
    - e.g., 75, 150, 300, ..., 9600 bps.
        

#### **Computer Network Transmission Rates:**

- Based on multiples/submultiples of **64 kbps** (e.g., **ISDN**).
    

#### **Error Control Techniques in Modems:**

1. **ARQ (Automatic Repeat Request):**
    
    - Uses a **buffer** to hold data until it is acknowledged or retransmission is requested.
        
    - Ensures **no data loss** before validation.
        
2. **Forward Error Correction (FEC):**
    
    - Used in **fast modems (9600–19200 bps)**
        
    - Adds **redundant bits** to detect and correct errors.
        

---

### **Baseband Modems**

#### **Definition:**  
Devices that transmit **unmodulated** digital signals over physical lines.

#### **Operation:**

- Filters digital signals to remove high-frequency content.
    
- Transmits directly over the medium **without modulation**.
    
- Suitable for **short distances** but supports **data rates up to 192 kbps**.
    

---

### **Codec (Coder/Decoder)**

#### **Function:**  
Converts **analog signals** into **digital form** for storage and transmission, and back to analog at the receiver.

#### **Process:**

1. Analog → Digital:
    
    - Signal is **quantized** into an equivalent **bit stream**.
        
2. Digital → Analog:
    
    - The **bit stream is decoded** back to an analog signal.
        

#### **Challenges:**

- Repeated digital patterns can create **spectral peaks**, leading to interference.
    

**Solution – Scrambling:**

- The **bit stream is randomized** by:
    
    - **Reordering message digits**
        
    - Using a **multi-stage shift register** for encoding and decoding
        

---

### Final Takeaways

✔ PSTN uses modulation to efficiently transmit analog signals over long distances.  
✔ Modems convert digital data into analog form and vice versa, categorized by speed and technique.  
✔ Data error correction is vital in noisy environments: ARQ holds data; FEC adds redundant bits.  
✔ Baseband modems avoid modulation, ideal for direct, short-range high-speed transmission.  
✔ Codecs handle analog–digital conversion, using scrambling to prevent interference in adjacent channels.

---

## **The Modern Modem**

### **Definition:**  
A modern modem is a communication device that converts digitally coded information into a form suitable for transmission over telephone networks. It supports duplex operation—allowing data transmission in both directions simultaneously.

### **Main Function:**

- Enables two-way digital communication over traditional two-wire telephone lines.
    
- Performs more than just conversion—it includes features that improve speed, accuracy, and reliability.
    

### **Transmission Method:**

- **For bit speeds up to 1200 bps**:  
    Utilizes **Frequency Division Multiplexing (FDM)**—the full telephone bandwidth is divided for both transmission directions.
    

### **Additional Features:**

- **Echo Cancellation**: Adaptive circuits in each receiver cancel self-interference and echoes.
    
- **Equalization Filters**: Minimize distortion from the transmission medium.
    
- **Data Compression & Expansion**: Enhance efficiency and reduce required bandwidth.
    
- **Automatic Answering Facilities**: Allow unattended connections.
    
- **Bit Rate Switching & Speed Recognition**: Adjusts automatically based on connection speed.
    
- **Frequency-Agile Modems**: Automatically change frequencies for optimal performance.
    
- **Facsimile Support**: Enables fax machine connectivity.
    
- **Microprocessor Integration**: All enhancements are coordinated by an internal microprocessor.

---

**Final Takeaways**  
✔ The modern modem is more than a converter—it manages duplex communication and includes enhancements for speed and quality.  
✔ It uses **frequency division multiplexing** for efficient use of bandwidth.  
✔ Echo cancellation and equalization improve signal clarity.  
✔ Additional features like compression, auto-answer, and adaptive speed make it robust for various communication needs.  
✔ All functionality is powered by an internal **microprocessor**, enabling smarter transmission.

---
## **Difference Between Multiplexing, Concentration, Grooming, and Consolidation**

#### **Definition**:

- **Multiplexing**: A method used to combine multiple signals or data streams into one for efficient transmission over a shared medium.
    
- **Concentration**: Uses a concentrator to process and compress data streams from multiple sources before combining.
    
- **Grooming**: Groups mixed digital signals (like speech, video, data) and separates them into uniform output streams.
    
- **Consolidation**: Combines valid data from multiple input channels into one by removing empty packets.
    

#### **Function**:

- **Multiplexing**: Shares bandwidth/time between devices to reduce cost and optimize usage.
    
- **Concentration**: Compresses data by eliminating redundancy and expands it back at the destination.
    
- **Grooming**: Organizes and filters different signal types into unified output channels.
    
- **Consolidation**: Reassembles meaningful data from various channels into a single, continuous data stream.
    

#### **Technique**:

- **Multiplexing**: Can be done via software (compute network) or hardware (multiplexing units).
    
- **Concentration**: Performs data processing like blank space removal and code compression.
    
- **Grooming**: Sorts and separates different signal types within digital packets.
    
- **Consolidation**: Tracks and logs which packets are removed for accurate reconstruction.
    

#### **Data Output:**

- **Multiplexing**: Combined signal preserving individual data integrity.
    
- **Concentration**: Compressed version of the original data with space removed.
    
- **Grooming**: Stream of one type of media (e.g., all audio, all video).
    
- **Consolidation**: A refined, complete data stream with minimal redundancy.
    

---

### **Comparison Between FDM, TDM, and CDM (Types of Multiplexing)**

#### **Definition**:

- **FDM (Frequency Division Multiplexing)**: Divides bandwidth into separate frequency bands.
    
- **TDM (Time Division Multiplexing)**: Allocates time slots to each data stream on a shared channel.
    
- **CDM (Code Division Multiplexing)**: Assigns a unique code to each data stream for simultaneous transmission.
    

#### **Function**:

- **FDM**: Shares a line by separating signals by frequency.
    
- **TDM**: Shares time on the same channel.
    
- **CDM**: Shares both time and frequency using code-based differentiation.
    

#### **Usage**:

- **FDM**: Common in broadband and analog systems.
    
- **TDM**: Suitable for digital systems like TV and radio.
    
- **CDM**: Secure communication, originally used by the military.
    

#### **Signal Handling:**

- **FDM**: Each signal has its frequency band.
    
- **TDM**: Each signal transmits in assigned time slots.
    
- **CDM**: All signals occupy the same spectrum but are separated by codes.
    

#### **Security:**

- **FDM & TDM**: Basic multiplexing, less secure.
    
- **CDM**: Encrypted, uses pseudo-random codes.
    

---

### **Broadband Transmission Solutions**

#### **Problem:**

- **Shared Frequency Issue**: Transmitting and receiving frequencies must differ, modems need to switch roles.
    

#### **Solution 1: Frequency-Agile Modems**

- **Function**: Switch operating frequencies via signals from a central controller.
    

#### **Solution 2: Headened Device**

- **Function**: Translates frequencies for reception so modems can use fixed frequencies.
    

---

### **Final Takeaways**

✔ **Multiplexing** allows multiple data streams to share a single channel.  
✔ **Concentrators** compress data by removing redundancies and blank spaces.  
✔ **Grooming** cleans up mixed signals and sorts them into distinct media streams.  
✔ **Consolidation** creates a single clean data stream from multiple input channels.  
✔ **FDM** splits bandwidth by frequency, **TDM** by time slots, **CDM** by codes.  
✔ **CDM** provides encrypted, interference-resistant transmission.  
✔ **Broadband systems** require smart modem coordination—via agile modems or a headened device.

---

## **Difference Between Baseband Signaling and Broadband Signaling**

### **Definition:**

- **Baseband Signaling**: Transmits digital data over the entire capacity of a medium using a single 0 or 1 bit at a time.
    
- **Broadband Signaling**: Uses modulation techniques to carry multiple signals over different frequency bands.
    

### **Application:**

- **Baseband**: Used in point-to-point connections and TDM systems.
    
- **Broadband**: Used for FDM-based systems and long-distance or high-capacity communication.
    

### **Signal Handling:**

- **Baseband**: Only one digital signal at a time on the transmission line.
    
- **Broadband**: Multiple signals coexist simultaneously via different frequencies.
    

### **Limitation:**

- **Baseband**: Transmission fails if two devices send data simultaneously.
    
- **Broadband**: Requires frequency coordination but supports parallel communication.
    

---

## **Comparison Between Synchronous TDM and Statistical TDM**

### **Definition:**

- **Synchronous TDM**: Allocates fixed time slots to each channel in a rotating, predictable sequence.
    
- **Statistical TDM**: Dynamically assigns time slots only to active channels based on real-time data needs.
    

### **Efficiency:**

- **Synchronous TDM**: Less efficient; time slots may be unused if a channel has no data.
    
- **Statistical TDM**: More efficient; avoids wastage by skipping inactive channels.
    

### **Bandwidth Usage:**

- **Synchronous TDM**: Bandwidth is permanently divided, causing potential idle time.
    
- **Statistical TDM**: Bandwidth is shared flexibly based on demand.
    

### **Synchronization:**

- **Synchronous TDM**: Requires tight synchronization between sender and receiver using synchronizing digits.
    
- **Statistical TDM**: Needs less rigid synchronization, as slot assignments vary.
    

---

## **Baseband Signaling: Challenges and Considerations**

### **Transmission Limitations:**

- Only one device can transmit at a time.
    
- Simultaneous transmissions lead to data corruption.
    

### **Requirements:**

- Precise timing and signal recognition are essential.
    
- Must identify data type and duration clearly.
    

### **Network Issues:**

- LANs using baseband must handle transmission conflicts.
    
- Complex protocols are needed to detect and manage simultaneous attempts.
    

---

## **Choice of Multiplexing Techniques**

### **Techniques:**

- **Bit-Interleave Multiplexers**: Each time slot holds 1 bit; used with synchronous sources.
    
- **Character-Interleave Multiplexers**: Suited for start-stop character-based systems.
    

### **Use Cases:**

- **Bit-Interleave**: High-speed, low-latency environments like VDUs.
    
- **Character-Interleave**: Slower, asynchronous communication systems.
    

### **Additional Needs:**

- Synchronous systems require time-slot synchronization.
    
- Channels must operate at the same speed for orderly rotation.
    
- Frames with synchronizing digits are used to maintain sequence integrity.
    

---

### Final Takeaways

✔ **Baseband signaling** uses the entire bandwidth for one signal at a time—simple but prone to data conflict.  
✔ **Broadband signaling** enables multiple parallel signals using frequencies—efficient for high-capacity links.  
✔ **Synchronous TDM** wastes bandwidth with fixed time slots, while **Statistical TDM** uses bandwidth on demand.  
✔ Proper **multiplexing technique choice** depends on speed, synchronization, and whether bit or character data is being used.  
✔ TDM systems must maintain timing and synchronization to prevent data loss.

---

## **Difference Between AM, FM, and PM Modulation Techniques**

### **Definition:**

- **AM (Amplitude Modulation)**: Varies the amplitude of the carrier wave to represent 1s and 0s.
    
- **FM (Frequency Modulation)**: Alters the frequency of the carrier to represent binary data.
    
- **PM (Phase Modulation)**: Changes the phase of the carrier to encode data.
    

### **How It Works:**

- **AM**: A '1' is the presence of a signal for 3 cycles; '0' is no signal.
    
- **FM**: A '0' is the original frequency, '1' is a higher frequency (closer-spaced cycles).
    
- **PM**: A '1' changes the phase of the wave; '0' keeps the phase unchanged.
    

### **Carrier Signal Use:**

- **AM**: Signal presence/absence indicates data.
    
- **FM**: Two different frequencies represent binary data.
    
- **PM**: Uses a single frequency; changes only phase at bit transitions.
    

### **Advantages:**

- **AM**: Simple to design.
    
- **FM**: Immune to noise; signal is always present.
    
- **PM**: Only one frequency used; easy to detect carrier loss.
    

### **Disadvantages:**

- **AM**: Noise easily affects amplitude; no signal = 0.
    
- **FM**: Needs 2 frequencies; circuit must detect both.
    
- **PM**: Complex circuit design for phase changes.
    

---

## **Modulation Techniques in Modems**

### **Common Modem Modulation Types:**

- **FSK (Frequency Shift Keying)**: Frequency-based modulation for digital data.
    
- **QPSK (Quadrature Phase Shift Keying)**: Phase-based modulation with four phase states.
    
- **QAM (Quadrature Amplitude Modulation)**: Combines amplitude and phase changes for more data per signal.
    

### **Modern Use:**

- Modems use combinations of FSK, QPSK, and QAM for higher data transfer rates (e.g., 14.4 Kbps+).
    
- Includes **compression** to optimize throughput.
    

---

## **Comparison: Simplex, Half Duplex, and Full Duplex FSK**

### **Frequency Shift Keying (FSK)**

- Encodes digital data as different frequencies.
    

---

### **Simplex / Half Duplex FSK:**

- **Single carrier (1170 Hz)** used for one-way communication.
    
- **Mark (1)**: 1270 Hz; **Space (0)**: 1070 Hz.
    
- Used in simple modem systems.
    

---

### **Full Duplex FSK:**

- **1170 Hz** and **2125 Hz** carriers used.
    
- **Originate Modem**: Transmits at 1170 Hz, receives at 2125 Hz.
    
- **Answer Modem**: Transmits at 2125 Hz, receives at 1170 Hz.
    
- Allows simultaneous send/receive (2-way communication).
    
- **Limitation**: Only effective up to 300 baud.
    

---

## **Why FSK Isn't Used for High-Speed Modems**

### **Limitations:**

- Higher speeds need more bandwidth.
    
- Frequency bands (Mark/Space) must be farther apart.
    
- Prevents **crosstalk** (interference).
    
- Present phone lines limit to **1200 baud** (Half Duplex).
    

---

## **Final Takeaways**

✔ **Modulation** transforms digital data into analog signals using AM, FM, or PM.  
✔ **AM** is simple but noise-sensitive. **FM** is noise-resistant but requires more frequencies. **PM** uses one frequency but is circuit-heavy.  
✔ **FSK**, **QPSK**, and **QAM** are common in modems.  
✔ **FSK** enables both **Half Duplex** and **Full Duplex** transmission using distinct frequency pairs.  
✔ Higher data rates need **more bandwidth**, limiting FSK for modern high-speed modems.

---

## **Difference Between FSK and QPSK Modulation**

### **Definition:**

- **FSK (Frequency Shift Keying)**: Modulates data by shifting between two distinct frequencies.
    
- **QPSK (Quadrature Phase Shift Keying)**: Modulates data by shifting the phase of the carrier signal using four distinct phase angles.
    

### **Encoding:**

- **FSK**: Each frequency represents either a binary 1 or 0.
    
- **QPSK**: Each phase change encodes two bits of data using 4 unique phase shifts (Quad-level PSK).
    

### **Transmission:**

- **FSK (Full Duplex)**:
    
    - Originate modem: 1170 Hz transmit, 2125 Hz receive.
        
    - Answer modem: 2125 Hz transmit, 1170 Hz receive.
        
- **QPSK**:
    
    - Originate modem: Transmits at 1200 Hz, receives on 2400 Hz.
        
    - Answer modem: Receives at 1200 Hz, transmits on 2400 Hz.
        

### **Baud Rate:**

- **FSK**: Typically 300 baud.
    
- **QPSK**: Uses 600 baud with differential encoding.
    

### **Usage:**

- **FSK**: Simplex/Half Duplex or low-speed Full Duplex.
    
- **QPSK**: Bell 212A, V.22 standards—1200 bps Full Duplex.
    

---

## **What Is a Frame?**

### **Definition:**

- A **frame** is a group of binary digits, typically with added bits for control and checking.
    

### **Purpose:**

- Enables reliable transmission by organizing data into **sequences** that are easy to manage and verify at the receiving end.
    

### **Techniques Involving Frames:**

- Frames are fundamental in **modulation** and **multiplexing** techniques.
    
- Framing is essential for both **FDM** and **TDM** transmission systems.
    
- **Statistical TDM** allows variable-length frames for better bandwidth efficiency.
    

---

## **Data Communication Over Telephone Networks**

### **Key Concepts:**

- **Modem** = **Modulator + Demodulator**
    
    - Modulates digital data to analog for transmission.
        
    - Demodulates received analog signal back into digital form.
        

### **Modes of Operation:**

- **Duplex**: Both ends transmit and receive simultaneously.
    
- **Half Duplex**: Each end can send and receive, but not at the same time.
    
- **Simplex**: Data flows in only one direction.
    

### **Limitations of Early Modems:**

- **300 bps Full Duplex** or **1200 bps Half Duplex** over PSTN lines.
    
- Limited by **bandwidth** and **signal quality** of analog telephone lines.
    

---

## **Final Takeaways**

✔ **QPSK** is more advanced than FSK, encoding more bits per symbol using phase shifts.  
✔ **Frames** are essential data units used for structured transmission, allowing error-checking and synchronization.  
✔ **Telephone networks** required modems to convert digital signals for analog transmission, using simplex, half duplex, or full duplex modes.  
✔ **Early modem speeds** were limited due to the physical constraints of telephone lines.

---

## **Switching Techniques**

### **Key Concepts:**

- **Data Switching**: Movement of data from source to destination node through intermediary switching nodes.
    

---

### **1. Circuit Switching (e.g., PSTN)**

- **Dedicated Path** is established between source and destination **before** communication begins.
    
- Follows **3 Phases**:
    
    1. **Circuit Establishment**
        
    2. **Data Transfer**
        
    3. **Circuit Disconnection**
        
- **Set-up time** is required before data transmission.
    
- Suitable for **voice calls**, not optimal for bursty data.
    
- **Duplex communication** is typically used.
    
- Inefficient for short or idle communication, as resources remain allocated.
    

---

### **2. Message Switching**

- No dedicated path; messages are stored temporarily at intermediate nodes (**store and forward**).
    
- Each message carries **destination address**.
    
- Data is forwarded node by node until it reaches destination.
    
- **Slower than circuit switching**, but more efficient in bandwidth usage.
    

**Advantages**:

- No need for continuous dedicated path.
    
- Efficient for long messages and asynchronous communication.
    

---

### **3. Packet Switching**

- Message is **divided into smaller packets** (few thousand bits).
    
- Each packet includes destination and sequence number.
    
- Uses **store and forward** like message switching, but more efficient.
    
- Allows interleaving packets from multiple sources.
    
- Basis for modern networks like the **Internet**.
    

**Advantages**:

- **Low delay**, better bandwidth utilization.
    
- **Efficient memory usage** at nodes.
    
- Packets take independent paths → resilient to failure.
    

---

## **Final Takeaways**

✔ **Circuit Switching** sets a fixed path, ideal for continuous communication (like voice).  
✔ **Message Switching** is flexible, stores full message at each node, but slower.  
✔ **Packet Switching** is modern, faster, more efficient, and robust against failure.  
✔ **Store and forward** is a common technique in both message and packet switching.

## **Key Points**
- **Rule:** The maximum permissible transmission rate of  a message is directly proportional to signal power and inversely proportional to channel noise.
- **Aim:** Provide the highest possible transmission rate at the lowest possible power with the least possible noise.
- Bit serial transmission is normally just called serial transmission and is the chosen communications method in many computer peripherals.

## **Summary**

-