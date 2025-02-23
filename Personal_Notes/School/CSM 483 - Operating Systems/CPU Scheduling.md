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


## 🗝️ Key Terms


---

## 💡 Key Points

-
---
## ✨ Summary

-
---
## ❓Review Questions

-