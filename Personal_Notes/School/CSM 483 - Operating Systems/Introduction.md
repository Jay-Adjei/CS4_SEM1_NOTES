---
course:
  - CSM 483
tags: 
last topic: Storage Structure
next topic: Storage Structure
note to self:
---

2025-02-10 09:21

# Introduction

## Detailed Notes
### **What is an Operating system?**
A program that acts as an intermediary between a user of a computer and the computer hardware.
**Goals:** 
- Use the computer hardware in an efficient manner.
- Make the computer system convenient to use.
- Execute user programs and make solving user problems easier.

### **Computer System Architecture**
Components of the computer system:
- **Hardware**: provides basic computing resources(CPU, memory, i/o devices).
- **Operating System**: Controls and coordinates the use of hardware among various applications and users.
- **Application programs**: Define the ways in which the computing resources are used to solve the computing problems of the users(word processors, compilers, web browsers).
- Users: People, machines, other computers.
User -> Application programs -> Operating systems -> Computer hardware

### **Computer System Organization**
#### **Computer system operation**
- **Components**:
    
    - **CPU**: Processes data.
    - **Device Controllers**: Manage devices like disks, mouse, keyboard, etc.
    - **Memory**: Stores data shared between CPU and devices.
    - **System Bus**: Connects CPU, memory, and device controllers.
- **Operation**:
    
    - Devices and CPU share access to memory via the system bus.
    - They operate [[concurrently]], competing for memory access.

1. **Concurrency**: I/O devices and the CPU can operate simultaneously.
2. **Device Controllers**:
    - Manage specific device types.
    - Have local buffers for temporary data storage.
    - Use operating system device drivers to handle operations.
3. **Data Movement**:
    - The CPU transfers data between main memory and local buffers.
    - I/O involves moving data between the device and its controller's buffer.
4. **[[Interrupts]]**:
    - Device controllers notify the CPU of task completion by sending an interrupt signal.

### **Interrupt Handling**
- **Preserving CPU State**:
    
    - The operating system saves the CPU's current state (registers and program counter) to resume the task later.
- **Interrupt Identification**:
    
    - The system identifies the type of interrupt that occurred.
- **Action Determination**:
    
    - Specific code segments handle each type of interrupt, defining what actions to take.

### **Interrupt Drive Cycle**
![[interrupt-drive cycle.png]]
**Explanation:** 
1. **Initiate I/O**:
    
    - The CPU (via a device driver) starts an I/O operation.
2. **I/O in Progress**:
    
    - The I/O controller performs the requested operation (e.g., reading or writing data).
3. **Interrupt Generation**:
    
    - When the I/O is complete, input/output is ready, or an error occurs, the I/O controller sends an interrupt signal to the CPU.
4. **Interrupt Handling**:
    
    - The CPU detects the interrupt and stops its current task.
    - It transfers control to the **Interrupt Handler** to process the interrupt (e.g., retrieve data or handle the error).
5. **Resume Task**:
    
    - After handling the interrupt, the CPU resumes the previously interrupted task.

This cycle ensures that the CPU doesn't waste time waiting for I/O to complete, improving efficiency.

### **I/O Structure**
There are two ways to handle I/O operations:

1. **Synchronous I/O**:
    
    - The user program waits until the I/O operation is completed before continuing.
2. **Asynchronous I/O**:
    
    - The user program continues running without waiting for the I/O operation to finish.

#### **Synchronous I/O** (Waits for completion):

- CPU idles or waits for the I/O to finish:
    - **Wait instruction**: CPU remains idle until the next interrupt.
    - **Wait loop**: CPU keeps checking for I/O completion (contends for memory access).
- Only one I/O request is processed at a time (no simultaneous I/O).

#### **Asynchronous I/O** (Does not wait for completion):

- **System call**: Program requests the OS to handle I/O and notify upon completion.
- **Device-status table**:
    - Tracks all I/O devices (type, address, and state).
    - OS uses it to check device status and update when an interrupt occurs.


### **Storage Structure**
**Main Memory:**
- Primary Storage medium.
- Directly accessible by the CPU, , , and is .
- Uses random access
- Volatile (loses data when off)
- usually DRAM

**Secondary Memory:** 
- Functions as an extension of the main memory.
- Stored data permanently(Non-volatile).
- Has larger capacity

**Hard Disk Drive:**
- HDDs consist of rigid metal or glass platters coated with magnetic material to store data.
- The disk's surface is divided into **tracks**, which are further broken down into smaller units called **sectors**.
- A **disk controller** manages the logical interaction between the HDD and the computer, ensuring data can be read or written.

**Non-Volatile Memory:** Faster, nonvolatile storage that's gaining popularity due to better performance, capacity, and affordability.

### **Storage Definitions and Notation Review**
- **Bit**: Smallest storage unit (0 or 1).
- **Byte**: 8 bits, the smallest convenient storage unit.
- **Word**: A larger unit based on the computer’s architecture (e.g., 64 bits).
- **Storage Units**:
    - **KB**: 1,024 bytes
    - **MB**: 1,024 KB
    - **GB**: 1,024 MB
    - **TB**: 1,024 GB
    - **PB**: 1,024 TB
- Networking uses **bits**, while storage typically uses **bytes**.

### **Storage Hierarchy**
- **Storage Hierarchy**:
    
    - Storage systems are organized in a hierarchy based on three key factors:
        - **Speed**: How quickly data can be accessed.
        - **Cost**: The expense of storage per unit of capacity.
        - **Volatility**: Whether the storage retains data without power.
- **Caching**:
    
    - Caching involves copying frequently accessed data into a faster storage system to improve performance.
    - Main memory can act as a **cache** for secondary storage, allowing quicker data access.
- **Device Driver**:
    
    - Each device controller uses a **device driver** to manage Input/Output (I/O) operations.
    - The device driver provides a **uniform interface** for communication between the hardware controller and the operating system’s kernel.

### **Storage-Device Hierarchy**
![[storage device hierarchy.png]]

### **How A Modern Computer Works**
- **Von Neumann Architecture**:
    
    - The computer follows the **Von Neumann architecture**, which organizes processing, memory, and devices.
- **CPU (Central Processing Unit)**:
    
    - Executes the **instruction execution cycle**, fetching instructions and data from memory.
    - Uses a **cache** for faster access to frequently used data.
    - Handles **threads of execution** for processing tasks.
- **Memory**:
    
    - Stores both **instructions** (programs) and **data**.
    - Transfers information to the CPU for processing through **data movement**.
- **Devices**:
    
    - Interact with the system via **I/O requests**, **data transfer**, and **interrupts**.
    - Use **DMA (Direct Memory Access)** to transfer data directly to/from memory without continuous CPU involvement, improving efficiency.

### **Direct Memory Access Structure**
- **Purpose**:
    
    - **Direct Memory Access (DMA)** is designed for **high-speed I/O devices** to transfer data efficiently at speeds close to memory.
- **Operation**:
    
    - The **device controller** handles data transfer by moving blocks of data from buffer storage directly to main memory.
    - This process occurs **without involving the CPU**, freeing up the CPU for other tasks.
- **Interrupts**:
    
    - Instead of generating an interrupt for every byte transferred, DMA generates only **one interrupt per block**, reducing system overhead and improving efficiency.

### **Operating Systems Operations**
- **Bootstrap Program**:
    
    - A simple code that initializes the computer system and loads the **kernel** into memory to start the operating system.
- **Kernel Initialization**:
    
    - After loading, the kernel starts **system daemons**, which are background services running outside the kernel.
- **Interrupt-Driven Kernel**:
    
    - The kernel is designed to handle events through **interrupts**, which can come from hardware or software:
        - **Hardware Interrupts**: Triggered by devices (e.g., I/O operations).
        - **Software Interrupts (Traps or Exceptions)**:
            - Errors like division by zero.
            - Requests for system services via **system calls**.
            - Other issues, such as infinite loops or processes interfering with each other or the operating system.

### **Multiprogramming (Batch System)**
- **Multiprogramming** ensures the CPU stays busy by managing multiple jobs.
- A **subset of jobs** is loaded into memory, and one job is selected via **job scheduling**.
- If a job is idle (e.g., waiting for I/O), the OS switches to another job.

### **Multitasking (Timesharing)**
- **Definition**:
    
    - Timesharing is an extension of batch systems where the CPU switches between jobs so quickly that users can interact with each job while it is running, creating **interactive computing**.
- **Key Features**:
    
    - **Response Time**: Designed to be very fast, typically less than 1 second, to ensure smooth interaction.
    - **Processes**: Each user has at least one program (process) executing in memory at a time.
    - **CPU Scheduling**: Manages multiple jobs ready to run simultaneously, ensuring fairness and efficiency.
- **Memory Management**:
    
    - **Swapping**: Moves processes in and out of memory when they don’t fit entirely in physical memory.
    - **Virtual Memory**: Allows processes to execute even if they are not completely in memory by using disk space to simulate additional memory.

### **Memory Layout for Multi-programmed System**
![[memory layout.png]]
- **Memory Layout**:
    
    - In a multiprogrammed system, memory is divided between the **operating system (OS)** and **user processes**.
    - The **operating system** occupies the top portion of memory (higher memory addresses).
    - The remaining memory is allocated to **processes** (e.g., Process 1, Process 2, etc.), which are stacked in lower memory addresses.
- **Purpose**:
    
    - The layout ensures that multiple processes can coexist in memory, enabling **multiprogramming**.
    - The operating system manages memory allocation and ensures processes do not interfere with each other.

### **Dual Mode Operation**
- **Dual-Mode Operation**:
    
    - The operating system uses **dual-mode operation** to protect itself and system components.
    - It operates in two modes:
        - **User mode**: For regular user applications.
        - **Kernel mode**: For OS-level code and privileged instructions.
- **Mode Bit**:
    
    - A **mode bit** provided by hardware identifies the current mode:
        - **User mode**: Mode bit is set to "user".
        - **Kernel mode**: Mode bit is set to "kernel".
    - Ensures users cannot manually switch to kernel mode.
- **Mode Switching**:
    
    - When a **system call** is made, the mode switches to kernel for execution and reverts to user mode once the call is complete.
- **Privileged Instructions**:
    
    - Certain instructions are marked as **privileged** and can only be executed in kernel mode to maintain system security and stability.

### **Timer**
- A **timer** prevents processes from running indefinitely or hogging resources.
- The OS sets a **counter** (privileged instruction) that is decremented by the physical clock.
- When the counter reaches **zero**, it triggers an **interrupt** to regain control or terminate a process exceeding its time limit.
- The timer is configured before scheduling any process.

### **Process Management**
- A **process** is an active program in execution; a program itself is passive.
- A process needs resources like **CPU**, **memory**, **I/O**, and **initialization data** to execute.
- When a process ends, its resources are reclaimed.
- **Single-threaded processes** use one program counter for sequential execution, while **multi-threaded processes** use one program counter per thread.
- Systems manage many processes, achieving **concurrency** by sharing CPUs across processes and threads.

#### **Process Management Activities**
- Providing mechanisms for process synchronization.
- Providing mechanisms for deadlock handling.
- Suspending and resuming processes.
- Creating and deleting user and system processes.
- Providing mechanisms for process communication.

### **Memory Management**
- **Memory management** ensures that instructions and data required by programs are loaded into memory for execution.
- It optimizes **CPU usage** and enhances **user response times** by:
    - **Tracking** which parts of memory are in use.
    - **Deciding** which processes and data to move in/out of memory.
    - **Allocating/deallocating** memory dynamically as needed.

### **File System Management**
- The OS abstracts physical storage into logical units called **files** and manages various storage mediums with different properties (speed, capacity, data transfer rate, access method ie. sequential or random).
- **File-system management** organizes files into directories and enforces **access control** for security.
- Key activities include:
    - **Creating, deleting, and manipulating** files and directories.
    - **Mapping files** to storage devices.
    - **Backing up files** to ensure data stability.

### **Mass Storage Management**
- **Mass storage** is used to store data that doesn’t fit in main memory or needs to be retained long-term.
- Proper management is critical, as disk speed and algorithms impact overall system performance.
- Key **OS activities** include:
    - **Mounting/unmounting**, **free-space management**, and **storage allocation**.
    - **Disk scheduling**, **partitioning**, and **data protection**.

### **Caching**
- **Caching** temporarily copies data from slower to faster storage for quick access and is used across hardware, OS, and software.
- **Cache behavior**:
    - Checks faster storage (cache) first for data.
    - If data is present, it’s used directly; otherwise, it’s fetched, cached, and then used.
- **Key considerations**:
    - Cache is **smaller** than the storage being cached.
    - Effective **cache management** involves setting the right **cache size** and a **replacement policy**.

### **Characteristics of Various Types of Storage**
![[types of storage.png]]

### **Migration of Data from Disk to Storage**
- In multitasking environments, the system ensures the **most recent value** of data is used, no matter where it resides in the storage hierarchy (e.g., disk, memory, cache, or register).
- **Cache coherency** is critical in multiprocessor systems to ensure all CPUs have the latest data in their caches.
- Distributed systems face challenges with **multiple copies of data**, requiring advanced solutions (covered in Chapter 19).

### **I/o Subsystem**
- The I/O subsystem of the OS **abstracts hardware complexities** from users.
- Responsibilities include:
    - **Buffering**: Temporary storage for data during transfers.
    - **Caching**: Faster access by storing partial data.
    - **[[Spooling]]**: Overlaps output and input of different jobs.
    - **Device-driver interface**: Ensures compatibility and manages **specific hardware drivers**.

### **Protection and Security**


## Key Points
- Operating system is resource allocator and a control program making efficient use of hardware, and managing execution of user programs.
- The one program that runs at all times is the **kernel**, everything else is either a system program or an application program.
- OSes also include **middleware**, this is a set software frameworks that provide additional services to application developers such as databases, multimedia, and graphics.

## Summary

-