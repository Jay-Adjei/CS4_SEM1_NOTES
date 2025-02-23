---
course: 
status: Incomplete
last topic: 
next topic:
---

2025-02-21 17:58

# CPU Scheduling

## 📚Detailed Notes

### **Basic Concepts**

1. **Maximum CPU Utilization**

- Achieved through **multiprogramming**, allowing multiple processes to run simultaneously.

2. **CPU–I/O Burst Cycle**

- The process execution alternates between **CPU bursts** (processing) and **I/O bursts** (waiting for I/O operations).
- A **CPU burst** is when the CPU executes instructions.
- An **I/O burst** is when the process waits for input/output operations to complete.
- This cycle repeats throughout the process lifecycle.

3. **CPU Burst Distribution**

- The **distribution of CPU bursts** is critical because it affects system performance and scheduling efficiency.
- Short CPU bursts are more common, but long bursts can impact system responsiveness.

---

### **Final Takeaways**

✔ Maximum CPU utilization is achieved with **multiprogramming**.  
✔ Processes alternate between **CPU bursts** (execution) and **I/O bursts** (waiting).  
✔ The cycle of **CPU and I/O bursts** continues until process completion.  
✔ **CPU burst distribution** influences system performance and scheduling efficiency.

### **CPU Scheduler**

1. **Definition**

- The **CPU scheduler** selects processes from the **ready queue** and allocates a CPU core for execution.
- The **ready queue** can be ordered in different ways based on scheduling algorithms.

2. **Scheduling Decisions** CPU scheduling occurs when a process:
	- **Switches from Running to Waiting:** Example: I/O request.
	- **Switches from Running to Ready:** Example: Preemption by a higher-priority process.
	- **Switches from Waiting to Ready:** Example: I/O completion.
	- **Terminates:** Process finishes execution.
    
3. **Choice in Scheduling**:
	- **No Choice:** In cases **1** and **4**, the CPU must select a new process if available.
	- **Choice Available:** In cases **2** and **3**, the CPU scheduler can decide whether to switch processes.

---

### **Final Takeaways**

✔ The **CPU scheduler** selects processes from the **ready queue** for CPU execution.  
✔ Scheduling decisions occur when a process waits, becomes ready, or terminates.  
✔ No scheduling choice for **Running → Waiting** and **Termination** states.  
✔ Choice is available for **Running → Ready** and **Waiting → Ready** states.

---

### **Preemptive and Nonpreemptive Scheduling**

1. **Definition**

- **Nonpreemptive Scheduling:** CPU scheduling occurs only when:
    - A process **switches from running to waiting**.
    - A process **terminates**.
    - Once a process has the CPU, it keeps it until it finishes or waits.
- **Preemptive Scheduling:** CPU scheduling can occur in all cases:
    - **Running to Waiting**, **Running to Ready**, **Waiting to Ready**, and **Termination**.
    - The CPU can be taken from a process if a higher-priority process becomes available.

1. **Modern OS Usage**

- Most modern operating systems (Windows, macOS, Linux, UNIX) use **preemptive scheduling** because it improves system responsiveness and multitasking.

---

### **Final Takeaways**

✔ **Nonpreemptive scheduling** allows a process to hold the CPU until it finishes or waits.  
✔ **Preemptive scheduling** enables the CPU to switch between processes as needed.  
✔ Modern systems favor **preemptive scheduling** for better performance and responsiveness.

---
### **Preemptive Scheduling and Race Conditions**

1. **Definition**

- **Race Condition:** Occurs when multiple processes access shared data, and the outcome depends on the sequence of their execution.
- **Cause in Preemptive Scheduling:**
    - One process is preempted while updating shared data.
    - The second process reads the data before the first finishes, causing **inconsistent data**.

1. **Example**

- Process A updates shared data.
- Process A is preempted before finishing.
- Process B reads the data, which is incomplete or incorrect.

---

### **Final Takeaways**

✔ **Preemptive scheduling** can lead to **race conditions** when processes share data.  
✔ **Data inconsistency** occurs if one process is preempted before completing its update.  
✔ Synchronization mechanisms are essential to prevent **race conditions** in concurrent systems.

---
### **Dispatcher**

1. **Definition**

- The **Dispatcher** is a module that gives control of the CPU to the process selected by the **CPU Scheduler**.

1. **Functions of the Dispatcher**

- **Switching Context:** Saves the state of the current process and loads the state of the next process.
- **Switching to User Mode:** Changes the CPU from kernel mode to user mode.
- **Jumping to User Program:** Restarts the next process at the correct instruction location.

1. **Dispatch Latency**

- **Dispatch Latency:** The time taken by the dispatcher to **stop one process** and **start another**. It includes the time needed for context switching, switching to user mode, and resuming execution.

---

### **Final Takeaways**

✔ The **Dispatcher** transfers CPU control from one process to another.  
✔ Key tasks include **context switching**, switching to **user mode**, and resuming the program.  
✔ **Dispatch Latency** is the time delay in switching between processes.  
✔ Lower **dispatch latency** improves system responsiveness.

---
### **Scheduling Criteria**

1. **CPU Utilization**

- The goal is to keep the CPU as busy as possible to maximize efficiency.

1. **Throughput**

- The number of processes that complete execution per unit of time.

1. **Turnaround Time**

- The total time taken to execute a particular process from submission to completion.

1. **Waiting Time**

- The time a process spends waiting in the **ready queue** before execution.

1. **Response Time**

- The time from when a request is submitted until the system produces the first response (not including output generation).

---

### **Final Takeaways**

✔ **CPU Utilization** measures how efficiently the CPU is used.  
✔ **Throughput** measures system performance based on process completion.  
✔ **Turnaround Time** indicates the total execution time of a process.  
✔ **Waiting Time** reflects process delays in the **ready queue**.  
✔ **Response Time** measures system responsiveness from request to initial response.

---
### **Scheduling Algorithm Optimization Criteria**

1. **Maximize CPU Utilization**

- Ensure the CPU remains as busy as possible to optimize system performance.

1. **Maximize Throughput**

- Increase the number of processes that complete execution within a given time frame.

1. **Minimize Turnaround Time**

- Reduce the total time taken from process submission to completion.

1. **Minimize Waiting Time**

- Limit the time processes spend waiting in the **ready queue**.

1. **Minimize Response Time**

- Decrease the time from when a process request is submitted until the first response is produced.

---

### **Final Takeaways**

✔ Scheduling algorithms aim to maximize **CPU utilization** and **throughput**.
✔ They also strive to minimize **turnaround time**, **waiting time**, and **response time** for better system performance and user experience.

---
### **Multilevel Queue and Multilevel Feedback Queue Scheduling**

#### **Multilevel Queue Scheduling**

- **Ready Queue:** Divided into multiple queues based on process characteristics.
- **Key Parameters:**
    - Number of queues.
    - Scheduling algorithm for each queue.
    - Method to assign processes to specific queues.
    - Scheduling among queues.
- **Priority Scheduling:** Highest priority queue is scheduled first. Lower-priority queues are only scheduled if higher-priority queues are empty.
- **Process Prioritization:**
    - Real-time processes (highest priority).
    - System processes.
    - Interactive processes.
    - Batch processes (lowest priority).

**Final Takeaways** ✔ Multiple queues categorize processes based on priority.  
✔ The highest-priority queue is always served first.  
✔ Different scheduling algorithms can be applied within each queue.

---

#### **Multilevel Feedback Queue Scheduling**

- **Process Movement:** Processes can move between queues.
- **Key Parameters:**
    - Number of queues.
    - Scheduling algorithm for each queue.
    - Conditions to upgrade or demote processes.
    - Method to assign processes to queues.
    - Aging technique to prevent starvation.

**Example:**

- **Three Queues:**
    - **Q0:** Round Robin (RR) with 8ms quantum.
    - **Q1:** RR with 16ms quantum.
    - **Q2:** First-Come-First-Served (FCFS).
- **Scheduling Process:**
    - Process starts in **Q0** with 8ms quantum.
    - If not finished within 8ms, it moves to **Q1** with a 16ms quantum.
    - If still incomplete, it moves to **Q2** with FCFS scheduling.

**Final Takeaways** ✔ Processes can change queues based on CPU bursts.  
✔ Round Robin is used in higher-priority queues with short time quanta.  
✔ Longer processes are eventually moved to FCFS in the lowest-priority queue.  
✔ Aging prevents starvation by promoting long-waiting processes.

---

**Differences Between Multilevel Queue and Multilevel Feedback Queue**

- **Multilevel Queue:** Fixed assignment of processes to queues, no movement between queues.
- **Multilevel Feedback Queue:** Processes can move between queues based on behavior and time spent waiting.
---
### **Thread Scheduling**

1. **User-Level vs. Kernel-Level Threads**
    
    - **User-Level Threads:** Managed by a thread library at the user level.
    - **Kernel-Level Threads:** Managed by the operating system kernel.
2. **Scheduling Concepts**
    
    - **Process-Contention Scope (PCS):**
        - Scheduling competition is **within a process**.
        - The thread library selects threads to run on **Lightweight Process (LWP)**.
        - Typically uses **priority** set by the programmer.
    - **System-Contention Scope (SCS):**
        - Scheduling competition is **among all threads** in the **system**.
        - The kernel selects threads to run on available CPU cores.
3. **Thread Models**
    
    - **Many-to-One:** Multiple user-level threads map to a single kernel thread.
    - **Many-to-Many:** Multiple user-level threads map to multiple kernel threads, allowing concurrency.

---

### **Final Takeaways**

✔ **PCS** schedules threads within a process, often based on priority.  
✔ **SCS** schedules threads system-wide, competing for CPU cores.  
✔ **User-level threads** are faster but lack kernel support, while **kernel-level threads** offer true parallelism.  
✔ **Many-to-One** models limit concurrency, whereas **Many-to-Many** models enhance performance by utilizing multiple CPUs.

---
### **Difference Between a Thread and a Process**

#### **1. Definition:**

- **Process:** An independent program in execution with its own memory space and system resources.
- **Thread:** A smaller execution unit within a process, sharing memory with other threads of the same process.

#### **2. Memory:**

- **Process:** Has its own memory space (code, data, stack, heap).
- **Thread:** Shares memory (code, data, heap) with other threads of the same process but has its own stack.

#### **3. Communication:**

- **Process:** Requires Inter-Process Communication (IPC) like pipes, sockets, and shared memory.
- **Thread:** Can communicate directly within the same process using shared memory.

#### **4. Overhead:**

- **Process:** Higher overhead due to context switching and separate memory allocation.
- **Thread:** Lower overhead since threads share resources and need minimal context switching.

#### **5. Creation Time:**

- **Process:** Slower creation because of separate memory allocation.
- **Thread:** Faster creation as it shares memory with its parent process.

#### **6. Crash Impact:**

- **Process:** If a process crashes, it does not affect other processes.
- **Thread:** If a thread crashes, it can crash the entire process.

#### **7. Example:**

- **Process:** Opening a browser or running a database server.
- **Thread:** Multiple browser tabs (threads within the browser process), or parallel execution of SQL queries.

---

### **Final Takeaways**

✔ **Processes** are independent, with separate memory and higher overhead.  
✔ **Threads** are lightweight, sharing memory within a process and faster to create.  
✔ Crashing a **process** is isolated, while a **thread** crash affects the entire process.  
✔ **Threads** offer better performance for tasks requiring shared memory and quick communication.

---
### **Multiple-Processor Scheduling**

1. **Definition:**

- Scheduling becomes more complex when multiple CPUs are available, involving various architectures like multicore CPUs, multithreaded cores, NUMA systems, and heterogeneous multiprocessing.

1. **Symmetric Multiprocessing (SMP):**

- Each processor is self-scheduling.
- Threads can be in a **common ready queue** shared by all cores or each core may have its **private queue** of threads.

1. **Multicore Processors:**

- Multiple processor cores are placed on the same physical chip, making them faster and more power-efficient.
- Multiple threads per core use **memory stall cycles** to progress another thread during memory retrieval.

1. **Multithreaded Multicore System:**

- Each core handles more than one hardware thread.
- If one thread experiences a memory stall, the system switches to another thread, improving efficiency.

1. **Chip-Multithreading (CMT):**

- Assigns multiple hardware threads to each core (e.g., Intel’s **hyperthreading**).
- A quad-core system with two hardware threads per core appears as **eight logical processors** to the OS.

1. **Two Levels of Scheduling:**

- **Level 1:** OS selects which software thread runs on a logical CPU.
- **Level 2:** Each core decides which hardware thread runs on its physical core.

1. **Load Balancing:**

- Keeps all CPUs evenly loaded for efficiency.
- **Push migration:** Periodic tasks push processes from overloaded CPUs.
- **Pull migration:** Idle processors pull tasks from busy processors.

1. **Processor Affinity:**

- Threads tend to run on the same processor to benefit from cached data (**processor affinity**).
- **Soft affinity:** OS tries to keep a thread on the same processor (no guarantees).
- **Hard affinity:** Process specifies which processors it can run on.

1. **[[NUMA]] and CPU Scheduling:**

- **NUMA-aware** systems assign memory close to the CPU running the thread for faster access.

1. **Real-Time CPU Scheduling:**

- **Soft real-time systems:** Critical tasks have high priority but no guaranteed scheduling.
- **Hard real-time systems:** Tasks must be serviced within a deadline.

---

### **Final Takeaways**

✔ Multiple-processor scheduling enhances performance by balancing workloads across CPUs.  
✔ **SMP** allows each core to schedule independently, using shared or private queues.  
✔ **Multicore processors** with multiple hardware threads maximize efficiency, especially during memory stalls.  
✔ **Chip-multithreading (CMT)** enables each core to handle multiple hardware threads, boosting throughput.  
✔ **Load balancing** ensures efficient CPU usage through **push** and **pull migration**.  
✔ **Processor affinity** improves performance by keeping threads on the same CPU.  
✔ **NUMA-aware** scheduling reduces latency by assigning memory close to the CPU.  
✔ **Real-time systems** prioritize tasks based on urgency, ensuring deadlines are met.

---
### **Difference Between a Multithreaded Multicore System and a Multicore Processor**

1. **Multicore Processor**
    
    - A **multicore processor** has multiple independent CPU cores on a single chip.
    - Each core can execute its own tasks, allowing multiple programs or processes to run simultaneously.
    - Example: A quad-core processor has four separate cores that can run four different tasks at once.
2. **Multithreaded Multicore System**
    
    - A **multithreaded multicore system** takes the concept of multicore processors further by allowing each core to handle multiple threads simultaneously.
    - This is achieved using **hardware threads** (also known as logical processors or hyper-threading in Intel systems).
    - If one thread is waiting (e.g., during a memory stall), the core can switch to another thread, improving CPU utilization.
    - Example: A quad-core processor with **2 hardware threads per core** appears as **8 logical processors** to the operating system, effectively doubling the number of threads that can run in parallel.

---

### **Key Differences**

|**Feature**|**Multicore Processor**|**Multithreaded Multicore System**|
|---|---|---|
|**Number of Threads per Core**|One thread per core|Multiple threads per core (e.g., hyper-threading)|
|**Parallelism**|Parallelism is achieved by multiple cores|Higher parallelism by allowing multiple threads per core|
|**Utilization During Memory Stalls**|A core becomes idle during a memory stall|The core switches to another thread during a memory stall|
|**Performance**|Faster than a single-core system|Even faster because it reduces idle time during memory access|
|**Example**|Quad-core CPU = 4 simultaneous tasks|Quad-core CPU with 2 threads per core = 8 simultaneous tasks|

---

### **Final Takeaways**

✔ **Multicore processors** improve performance by having multiple cores execute tasks in parallel.  
✔ **Multithreaded multicore systems** further enhance performance by enabling each core to switch between multiple threads, reducing idle time and improving CPU efficiency.  
✔ **Hyper-threading** (by Intel) is a common example of multithreading within each core.  
✔ The combination of multiple cores and hardware threads provides **greater concurrency** and **faster task execution**.

---

## 🗝️ Key Terms

- **Multiprogramming:** Running multiple processes simultaneously to maximize CPU utilization.
- **CPU–I/O Burst Cycle:** Alternating periods of CPU execution and I/O waiting.
- **CPU Burst:** A period where the CPU is actively executing instructions.
- **I/O Burst:** A period where the process waits for input/output operations.
- **CPU Scheduler:** Selects processes from the ready queue for CPU execution.
- **Preemptive Scheduling:** The CPU can be taken from a process if a higher-priority process becomes available.
- **Nonpreemptive Scheduling:** A process keeps the CPU until it finishes or waits.
- **Race Condition:** Data inconsistency when processes share data and are interrupted before completing updates.
- **Dispatcher:** Module that hands control of the CPU to the scheduled process.
- **Dispatch Latency:** Time taken to stop one process and start another.
- **Turnaround Time:** Total time from process submission to completion.
- **Waiting Time:** Time a process spends in the ready queue.
- **Response Time:** Time from process request submission until the first response.
- **Multilevel Queue Scheduling:** Multiple queues with fixed process assignments and priority-based scheduling.
- **Multilevel Feedback Queue Scheduling:** Processes can move between queues based on behavior and waiting time.
- **Process-Contention Scope (PCS):** Scheduling competition within a process.
- **System-Contention Scope (SCS):** Scheduling competition among all system threads.
- **Symmetric Multiprocessing (SMP):** Each processor is self-scheduling.
- **Chip-Multithreading (CMT):** Multiple hardware threads per core (e.g., hyper-threading).
- **Processor Affinity:** Tendency of a thread to run on the same CPU to benefit from cached data.
- **NUMA (Non-Uniform Memory Access):** Assigns memory close to the CPU running the thread for faster access.
- **Real-Time Systems:** Must meet deadlines (soft real-time has no guarantee, hard real-time must meet deadlines).
- **Multithreaded Multicore System:** Each core can run multiple threads simultaneously.
- **Multicore Processor:** A chip with multiple independent CPU cores.

---

## 💡 Key Points

- **CPU Scheduling:**
    
    - **CPU–I/O Burst Cycle:** Processes alternate between CPU bursts and I/O bursts.
    - **CPU Scheduler:** Selects processes from the ready queue for execution based on scheduling algorithms.
    - **Dispatch Latency:** Must be minimized for better system responsiveness.
- **Scheduling Algorithms:**
    
    - **Preemptive Scheduling:** Allows the CPU to switch between processes for better responsiveness.
    - **Nonpreemptive Scheduling:** The CPU cannot be taken from a process once allocated.
- **Performance Metrics:**
    
    - **CPU Utilization:** Maximize CPU usage.
    - **Throughput:** Maximize the number of processes executed per time unit.
    - **Turnaround Time:** Minimize total execution time.
    - **Waiting Time:** Minimize waiting time in the ready queue.
    - **Response Time:** Minimize the delay in producing the first response.
- **Advanced Scheduling Methods:**
    
    - **Multilevel Queue:** Fixed queues with no process movement.
    - **Multilevel Feedback Queue:** Allows processes to move between queues to prevent starvation.
    - **Processor Affinity:** Threads prefer to run on the same processor for performance benefits.
    - **Load Balancing:** Distributes workload across processors (push and pull migration).
- **Thread Scheduling:**
    
    - **PCS:** Scheduling competition within a process (user-level threads).
    - **SCS:** Scheduling competition among all threads in the system (kernel-level threads).
- **Multiple-Processor Scheduling:**
    
    - **Symmetric Multiprocessing (SMP):** Each core schedules its own tasks independently.
    - **Chip-Multithreading (CMT):** Each core can run multiple hardware threads (hyper-threading).
    - **NUMA:** Memory is assigned close to the CPU running the thread to reduce latency.
- **Comparison of Systems:**
    
    - **Multicore Processor:** Each core can execute one thread.
    - **Multithreaded Multicore System:** Each core can execute multiple threads, improving performance during memory stalls.

---
## ✨ Summary

CPU scheduling is essential for maximizing system performance and ensuring efficient process execution. Processes alternate between **CPU bursts** (execution) and **I/O bursts** (waiting), and the **CPU scheduler** selects processes from the **ready queue** based on scheduling algorithms. Scheduling can be **preemptive** (interrupting processes) or **nonpreemptive** (process runs until it finishes or waits).

Performance is measured using metrics like **CPU utilization**, **throughput**, **turnaround time**, **waiting time**, and **response time**. Advanced methods like **Multilevel Queue** and **Multilevel Feedback Queue** improve scheduling efficiency, while **processor affinity** and **load balancing** optimize performance in multi-core environments.

**Thread scheduling** involves managing **user-level** and **kernel-level** threads, with competition occurring within processes (**PCS**) or system-wide (**SCS**). In **multiple-processor scheduling**, systems like **Symmetric Multiprocessing (SMP)** and **Chip-Multithreading (CMT)** enable better performance by running multiple threads per core and balancing workloads across CPUs. **NUMA-aware** systems improve memory access speed by assigning memory close to the CPU running the thread.

The difference between **Multicore Processors** and **Multithreaded Multicore Systems** lies in thread handling: multicore processors execute one thread per core, while multithreaded multicore systems allow each core to run multiple threads simultaneously, improving efficiency during memory stalls.

---
## ❓Review Questions

1. **Define the CPU–I/O burst cycle. Why is it important in CPU scheduling?**
2. **Explain the difference between preemptive and nonpreemptive scheduling. Which one is used in modern OS and why?**
3. **List and define five performance metrics used to evaluate scheduling algorithms.**
4. **Describe the role of the dispatcher and explain the concept of dispatch latency.**
5. **What is a race condition, and how can preemptive scheduling cause it? Provide an example.**
6. **Differentiate between Multilevel Queue and Multilevel Feedback Queue scheduling.**
7. **What is the difference between Process-Contention Scope (PCS) and System-Contention Scope (SCS)?**
8. **How does Symmetric Multiprocessing (SMP) work, and what are its benefits?**
9. **Explain Chip-Multithreading (CMT) and its advantage in CPU performance.**
10. **What is processor affinity? How do soft affinity and hard affinity differ?**
11. **Describe how NUMA-aware systems improve CPU performance.**
12. **What are the two levels of scheduling in a multithreaded multicore system?**
13. **Compare Multicore Processors and Multithreaded Multicore Systems. Give an example of each.**
14. **Why is load balancing essential in multiple-processor scheduling? Explain push migration and pull migration.**
15. **Differentiate between soft real-time systems and hard real-time systems.**