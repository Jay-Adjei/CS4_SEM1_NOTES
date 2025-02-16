---
course:
  - CSM 483
tags: 
last topic: Serial Communications
next topic: Kernel Data Structure
note to self: 
status: Completed
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
1. **Protection**:
    
    - Mechanisms provided by the OS to **control access** to system resources.
    - Ensures that processes and users interact with resources in an authorized way.
2. **Security**:
    
    - Defense mechanisms to safeguard the system from **internal and external attacks**.
    - Protects against threats like denial-of-service attacks, worms, viruses, identity theft, and unauthorized service access.
3. **User and Access Control**:
    
    - **User ID (UID)**:
        - Each user is assigned a unique identity (user ID) and associated security credentials.
        - The user ID is linked to the user's files and processes to enforce access control.
    - **Group ID (GID)**:
        - Users can belong to a group identified by a group ID.
        - Groups help manage permissions for a set of users, allowing collective access control for files and processes.
4. **Privilege Escalation**:
    
    - A mechanism that allows a user to temporarily **gain additional rights or privileges** by switching to another effective ID.
    - Used for administrative tasks but must be carefully controlled to avoid abuse.

### **Virtualization**
- **Definition**:
    
    - **Virtualization** allows one operating system (OS) to run applications or even other operating systems (**guest OSes**) within it. It is a significant and expanding industry.
- **Emulation**:
    
    - Used when the source CPU architecture differs from the target CPU (e.g., running PowerPC software on an Intel x86 system).
    - Emulation is typically **slow** because it translates instructions from one architecture to another.
    - When programs are not compiled to native code, **interpretation** is used instead, further slowing execution.
- **Virtualization**:
    
    - In contrast to emulation, virtualization assumes the **host and guest OSes** are natively compatible with the CPU.
    - Example: Running multiple **Windows XP guest OSes** on a native Windows XP **host OS** using virtualization software like VMware.
    - A **VMM (Virtual Machine Manager)** provides the necessary services to manage virtual machines.

- **Use Cases for Virtualization**:
    
    - **Running multiple OSes**: A single machine can run multiple operating systems for testing, exploration, or compatibility.
        - Example: An Apple laptop running **Mac OS X** as the host OS and **Windows** as a guest OS.
    - **Developing cross-platform apps**: Developers can test applications on different OSes without needing multiple physical systems.
    - **Quality Assurance**: Test applications across various OSes for reliability without maintaining multiple systems.
    - **Data Center Management**: Manage and execute multiple computing environments within data centers efficiently.
- **Virtual Machine Manager (VMM)**:
    
    - The **VMM** can run directly on hardware (natively), making it both the **host** and manager of virtual environments.
    - Examples of native VMMs include **VMware ESX** and **Citrix XenServer**, which do not rely on a general-purpose host OS.

### **Computing Environment Virtualization**
![[computing environments - virtualization.png]]
- **Non-Virtualized Environment (Diagram a)**:
    
    - In a traditional setup, processes interact directly with the **kernel**, which manages hardware resources like CPU, memory, and I/O devices.
    - A **programming interface** bridges processes and the kernel, allowing applications to utilize system resources.
- **Virtualized Environment (Diagram b)**:
    
    - The **Virtual Machine Manager (VMM)**, also known as a hypervisor, sits between the hardware and multiple virtual machines (VMs).
    - Each **VM** operates independently, with its own **kernel** and **processes**, as if it were running on separate hardware.
    - The VMM manages resource allocation and ensures isolation between VMs, enabling multiple operating systems to coexist on a single physical machine.

### **Distributed Systems**
- **Definition**:
    
    - A **distributed system** is a collection of separate systems (which may be heterogeneous) that are connected via a network.
- **Network**:
    
    - The **network** serves as the communication path for the systems, with **TCP/IP** being the most common protocol.
    - **LAN**: Small-scale (office/campus).
    - **WAN**: Large-scale (connects LANs).
    - **MAN**: City or regional coverage.
    - **PAN**: Personal device connections.
- **Network Operating System (NOS)**:
    
    - Provides features that allow systems to collaborate across the network.
    - Key functionalities include:
        - **Communication scheme**: Facilitates message exchange between systems.
        - Creates the **illusion of a single system** by integrating resources seamlessly.

### **Computer System Architecture**
- **Single-Processor Systems**:
    
    - Most computer systems use a **single general-purpose processor** to execute tasks.
    - Some systems also include **special-purpose processors** for specific tasks (e.g., graphics or network processing).
- **Multiprocessor Systems**:
    
    - These systems are becoming increasingly common and are also called **parallel systems** or **tightly-coupled systems**.
    - **Advantages**:
        1. **Increased throughput**: More work can be done simultaneously.
        2. **Economy of scale**: Shared resources reduce costs.
        3. **Increased reliability**: Graceful degradation (if one processor fails, others can continue working) or fault tolerance.
    - **Types of Multiprocessing**:
        1. **Asymmetric Multiprocessing**:
            - Each processor is assigned a specific task, and one processor may control others.
        2. **Symmetric Multiprocessing**:
            - All processors are treated equally, and each can perform all tasks.

### **Symmetric Multiprocessing Architecture**

![[symmetric multiprocessing architecture.png]]
- **Architecture Overview**:
    
    - In **symmetric multiprocessing (SMP)**, two or more processors are connected to a shared **main memory** and operate under the same operating system.
    - Each processor has its own **registers** and **cache** for storing temporary data and speeding up operations.
- **Processor Design**:
    
    - All processors in the system are equal and can perform any task.
    - They access **main memory** through a shared bus or connection, which allows them to collaborate and execute tasks efficiently.
- **Advantages**:
    
    - **Equal responsibility**: No processor has a specific role; all processors can handle any task.
    - **Resource sharing**: Shared memory allows communication and coordination between processors.

#### **Dual-Core Design**
![[Dual-Core Design.png]]
- **Dual-Core and Multicore Design**:
    
    - **Dual-core** refers to a single processor containing **two CPU cores** on the same chip.
    - Each core operates independently, with its own **registers** and **L1 cache** (Level 1 cache).
- **Cache Hierarchy**:
    
    - Both cores share a larger **L2 cache** (Level 2 cache), which acts as a bridge between the cores and the **main memory**.
    - This shared cache allows efficient communication and data access between cores.
- **System Design**:
    
    - Dual-core processors are part of **multicore systems**, where multiple chips or cores are integrated into a single system.
    - These systems can also include **chassis-based designs** that house multiple separate systems for scalability.

### **Non-Uniform Memory Access System**
![[NUMA.png]]
- **Definition of NUMA**:
    
    - In **Non-Uniform Memory Access (NUMA)** systems, each CPU has its own **local memory** that it can access faster than the memory connected to other CPUs.
    - CPUs are connected through an **interconnect network**, allowing them to access both local and remote memory.
- **Memory Access Characteristics**:
    
    - Accessing **local memory** (e.g., memory₀ for CPU₀) is faster because it is directly connected to the CPU.
    - Accessing **remote memory** (e.g., CPU₀ accessing memory₁) is slower because it involves the interconnect.
- **Advantages**:
    
    - NUMA improves **scalability** by allowing memory to be distributed across CPUs.
    - Reduces contention and bottlenecks associated with shared memory systems.
- **Use Cases**:
    
    - Commonly used in high-performance computing and [[systems requiring large-scale parallel processing]].

### **Clustered Systems**
- **Definition**:
    
    - Clustered systems involve multiple systems working together, similar to multiprocessor systems but using separate machines.
    - These systems often share storage via a **Storage Area Network (SAN)**.
- **High Availability**:
    
    - Clustered systems provide **high-availability services** that continue to operate even if one machine fails.
- **Types of Clustering**:
    
    - **Asymmetric Clustering**:
        - One machine is in **hot-standby mode**, ready to take over in case another machine fails.
    - **Symmetric Clustering**:
        - Multiple nodes run applications simultaneously and monitor each other for faults.
- **High-Performance Computing (HPC)**:
    
    - Some clusters are used for **HPC**, requiring applications to be designed with **parallelization** in mind for maximum performance.
- **Distributed Lock Manager (DLM)**:
    
    - Some clusters use a **DLM** to manage and prevent conflicting operations when multiple nodes access shared resources.

![[clustered systems.png]]
- **Components**:
    
    - **Multiple computers** are connected via an **interconnect network**.
    - These computers share access to a **Storage Area Network (SAN)**, which acts as centralized storage.
- **Operation**:
    
    - The **interconnect** allows the computers to communicate and coordinate tasks.
    - The **SAN** provides a shared storage resource that all computers can access simultaneously.
- **Purpose**:
    
    - This setup supports **high availability**, ensuring that if one computer fails, others can take over.
    - It also supports **parallel processing** in high-performance computing environments.

### **Computer Systems Environments**
### **Traditional Computing**

- **Description**:
    - General-purpose stand-alone machines (e.g., desktops, laptops).
    - Increasingly interconnected via the **Internet** and **wireless networks**.
- **Key Features**:
    - Use **portals** for accessing internal systems.
    - **Thin clients** serve as lightweight terminals for web-based applications.
    - **Firewalls** protect home systems from Internet attacks.

---

### **2. Mobile Computing**

- **Description**:
    - Includes **smartphones**, **tablets**, and similar handheld devices.
- **Key Features**:
    - Differ from traditional computers with added sensors like **GPS** and **gyroscopes**.
    - Enable apps for **augmented reality**.
    - Use **Wi-Fi** (IEEE 802.11) or **cellular networks** for connectivity.
    - Leaders: **Apple iOS** and **Google Android**.

---

### **3. Client-Server Computing**

- **Description**:
    - **Clients** (desktops, laptops, smartphones) request services from **servers**.
- **Key Features**:
    - **Compute-server systems**: Handle service requests (e.g., databases).
    - **File-server systems**: Manage file storage and retrieval.
- **Architecture**:
    - A network connects clients to the server.

---

### **4. Peer-to-Peer (P2P) Computing**

- **Description**:
    - A distributed system where all nodes are **peers**, with no distinction between clients and servers.
- **Key Features**:
    - Peers can act as both clients and servers.
    - Use a **discovery protocol** to locate services.
    - Examples: **Napster**, **Skype** (VoIP).

---

### **5. Cloud Computing**

- **Description**:
    - Provides **computing, storage, and apps as a service** via a network.
- **Key Features**:
    - Based on **virtualization**.
    - Example: **Amazon EC2** offers servers, virtual machines, and scalable storage.
- **Types of Cloud**:
    - **Public Cloud**: Accessible to anyone for a fee.
    - **Private Cloud**: Dedicated to a single organization.
    - **Hybrid Cloud**: Combination of public and private.
- **Service Models**:
    - **SaaS**: Software as a service (e.g., Google Docs).
    - **PaaS**: Platform as a service (e.g., app development environments).
    - **IaaS**: Infrastructure as a service (e.g., servers, storage).

---

### **6. Real-Time Embedded Systems**

- **Description**:
    - **Special-purpose systems** with strict timing constraints, often without traditional OSes.
- **Key Features**:
    - Perform specific tasks within fixed deadlines.
    - Use cases include medical devices, industrial robots, and automotive systems.

### **Free and Open-Source Operating Systems**
- **Definition**:
    
    - Open-source operating systems are distributed in **source-code format**, unlike **closed-source** or **proprietary** software, which is distributed as binaries.
- **Philosophy**:
    
    - Open-source counters **Digital Rights Management (DRM)** and **copy protection** restrictions in proprietary software.
    - It is supported by organizations like the **Free Software Foundation (FSF)**, which promotes freedom for users to run, study, share, and modify software under the **GNU Public License (GPL)**.
- **Examples**:
    
    - Popular open-source operating systems include:
        - **GNU/Linux**.
        - **BSD UNIX** (forms the core of **Mac OS X**).
    - These systems allow users to customize and use them freely.
- **Tools for Exploration**:
    
    - Open-source virtualization tools like:
        - **VMware Player** (free for Windows).
        - **VirtualBox** (free and open-source, available on many platforms).
    - These tools enable users to explore guest operating systems on their machines.

### **Kernel Data Structures**
- **Linked Lists**:
    
    - **Singly Linked List**: Each node points to the next node, with the last node pointing to `null`.
    - **Doubly Linked List**: Each node has pointers to both the next and previous nodes, allowing bidirectional traversal.
    - **Circular Linked List**: Similar to a singly linked list but the last node points back to the first, forming a loop.
- **Binary Search Tree**:
    
    - A tree where each node has a left child (smaller value) and a right child (greater value).
    - **Search Performance**:
        - Unbalanced tree: O(n).
        - Balanced tree (e.g., AVL, Red-Black Tree): O(log n).
- **Hash Maps**:
    
    - Created using **hash functions**, which map keys to values for quick lookup.
    - Hash functions ensure efficient data retrieval in constant time O(1) on average.
- **Bitmap**:
    
    - A **bitmap** is a string of `n` binary digits representing the status of `n` items.
    - Used in the kernel to efficiently manage resources (e.g., free or used memory blocks).
- **Kernel-Specific Data Structures**:
    
    - In Linux, these are defined in include files like:
        - `<linux/list.h>` for linked lists.
        - `<linux/rbtree.h>` for red-black trees.
        - `<linux/kfifo.h>` for FIFO buffers.

## Key Points
- Operating system is resource allocator and a control program making efficient use of hardware, and managing execution of user programs.
- The one program that runs at all times is the **kernel**, everything else is either a system program or an application program.
- OSes also include **middleware**, this is a set software frameworks that provide additional services to application developers such as databases, multimedia, and graphics.
- **Operating System Overview**:
    
    - Acts as an intermediary between users and computer hardware.
    - Goals: Efficient hardware usage, convenience, and user problem-solving.
- **Computer System Architecture**:
    
    - Components: Hardware, OS, application programs, users.
    - Interaction: Users -> Applications -> OS -> Hardware.
- **System Organization**:
    
    - Key components: CPU, memory, device controllers, and system bus.
    - Concurrency and interrupts improve efficiency and multitasking.
- **Interrupt Handling**:
    
    - CPU saves state, identifies interrupt type, and executes specific actions.
- **I/O Structures**:
    
    - **Synchronous I/O**: Waits for completion.
    - **Asynchronous I/O**: Continues execution while waiting for I/O.
- **Storage Hierarchy**:
    
    - Organized by speed, cost, and volatility.
    - Main memory is volatile, secondary storage is non-volatile.
- **Process and Memory Management**:
    
    - OS manages resources for processes and optimizes memory allocation.
- **File and Mass Storage Management**:
    
    - OS organizes files, directories, and manages storage for efficiency.
- **Virtualization**:
    
    - Allows multiple OSes to run on one system using virtual machines.
- **Computing Environments**:
    
    - Includes traditional, mobile, client-server, peer-to-peer, cloud, and real-time embedded systems.
- **Open-Source Operating Systems**:
    
    - Available in source-code form, allowing freedom to modify and use.
- **Kernel Data Structures**:
    
    - Includes linked lists, binary search trees, hash maps, and bitmaps for efficient system resource management.
## Summary
An **Operating System (OS)** acts as a bridge between users and computer hardware, enabling efficient resource utilization, ease of use, and solving user problems. It manages hardware (CPU, memory, I/O devices), facilitates process execution, and optimizes system performance through features like **interrupt handling**, **I/O structures**, and **storage management**.

The **system architecture** includes hardware (resources), the OS (controller), application programs (problem solvers), and users. Key components like the **CPU**, **memory**, and **device controllers** are interconnected via a **system bus**, allowing concurrent operations.

**Interrupt handling** ensures efficiency by saving the CPU state, identifying the interrupt type, and executing specific actions. For I/O, **synchronous I/O** waits for completion, while **asynchronous I/O** allows processes to continue execution, leveraging device drivers and status tables.

**Storage hierarchy** organizes data by speed, cost, and volatility. Main memory (volatile) provides quick access, while secondary storage (non-volatile) offers long-term data retention. Techniques like **caching** copy frequently accessed data to faster storage for better performance.

**Process management** involves allocating resources (CPU, memory, I/O) to active programs and achieving concurrency through scheduling and synchronization. **Memory management** tracks memory usage, decides process allocation, and dynamically adjusts memory as needed. The **file system** abstracts physical storage into logical units, managing files, directories, and access control.

Modern systems support **computing environments** like traditional desktops, mobile devices (smartphones/tablets), client-server models, peer-to-peer networks, cloud computing (e.g., Amazon EC2), and real-time embedded systems (e.g., medical devices). **Virtualization** allows multiple OSes to run on one system via virtual machines, enabling efficient resource use and testing.

**Kernel data structures** like linked lists, binary search trees, hash maps, and bitmaps efficiently manage system resources. Open-source OSes (e.g., Linux, BSD UNIX) provide flexibility and customization, supported by tools like **VirtualBox** for experimentation.

## Questions
- **Operating Systems**:
    
    - What are the primary goals of an operating system?
    - How does the OS act as an intermediary between the user and hardware?
- **Interrupts**:
    
    - What is the purpose of interrupts in improving system efficiency?
    - How does the CPU handle interrupts during execution?
- **I/O Structures**:
    
    - What is the difference between synchronous and asynchronous I/O operations?
- **Storage Management**:
    
    - How is storage organized in a hierarchy based on speed, cost, and volatility?
    - Why is secondary memory essential in modern computing?
- **Virtualization**:
    
    - How does virtualization differ from emulation?
    - What are the key use cases for virtualization in computing environments?
- **Kernel Data Structures**:
    
    - Why are linked lists, binary search trees, and hash maps important in kernel design?
    - How does a bitmap help in resource management?
- **Computing Environments**:
    
    - What are the main differences between client-server and peer-to-peer models?
    - How does cloud computing leverage virtualization for scalability?
- **Open-Source OS**:
    
    - What advantages do open-source operating systems offer compared to proprietary ones?
    - What are examples of tools used to explore open-source OSes?