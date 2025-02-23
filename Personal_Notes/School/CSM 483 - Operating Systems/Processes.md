---
course: 
status: Incomplete
last topic: 
next topic:
---

2025-02-21 10:48

# Processes

## 📚Detailed Notes

### **Process Concept**
1. **Definition**

- A process is a program in execution, progressing sequentially without parallel instruction execution.

2. **Components of a Process**

- **Text Section:** Contains program code.
- **Program Counter:** Tracks current execution position and processor registers.
- **Stack:** Holds temporary data such as function parameters, return addresses, and local variables.
- **Data Section:** Stores global variables.
- **Heap:** Allocates memory dynamically during runtime.

**Program vs. Process**

- A **program** is a passive entity (executable file), while a **process** is active.
- A program becomes a process when loaded into memory.
- Execution begins through GUI clicks or command-line inputs.
- A single program can create multiple processes (e.g., multiple users running the same application).

**Final Takeaways**  
✔ A process is a sequentially executed program.  
✔ Key components include the text section, program counter, stack, data section, and heap.  
✔ Temporary and dynamically allocated memory is managed through the stack and heap.
✔ A program is passive, becoming a process when executed.  
✔ Multiple processes can be created from one program.

### **Process In Memory**
![[process in memory.png]]

### **Memory Layout of a C Program**
![[c program.png]]

### **Process State**
A process changes states as it executes.

1. **New:** The process is being created.
2. **Running:** Instructions are actively executed by the CPU.
3. **Waiting:** The process is paused, waiting for an external event.
4. **Ready:** The process is ready to run, waiting for CPU availability.
5. **Terminated:** The process has finished execution.

---

### **Process State Transition**

- A process moves from **New** to **Ready** when created.
- From **Ready** to **Running** when assigned the CPU.
- Moves to **Waiting** if it requires an event.
- Returns to **Ready** when the event is resolved.
- Ends in **Terminated** once execution is complete.

---

### **Final Takeaways**

✔ A process has five states: New, Running, Waiting, Ready, and Terminated.  
✔ State transitions depend on CPU availability and external events.  
✔ The process lifecycle starts in **New** and ends in **Terminated**.

### **Process Control Block (PCB)**

A **Process Control Block (PCB)**, also called a **Task Control Block**, stores essential information about each process.

1. **Process State:** Indicates the current state (Running, Waiting, Ready, etc.).
2. **Process Number:** Unique identifier for the process.
3. **Program Counter:** Stores the address of the next instruction to execute.
4. **Registers:** Holds process-specific CPU registers.
5. **CPU Scheduling Information:** Includes process priority and queue pointers.
6. **Memory Management Information:** Tracks the memory allocated to the process.
7. **Accounting Information:** Records CPU usage, clock time, and time limits.
8. **I/O Status Information:** Lists allocated I/O devices and open files.

---

### **Role of the PCB**

- Acts as the process’s identity card, storing all essential data.
- Allows the operating system to **pause and resume** processes.
- Enables **context switching** by saving and restoring process information.

---

### **Final Takeaways**

✔ The PCB stores vital information such as state, program counter, and CPU registers.  
✔ It tracks scheduling priorities, memory limits, and I/O devices.  
✔ Essential for **context switching**, ensuring smooth multitasking.  
✔ Each process has a unique PCB, allowing the OS to manage multiple processes simultaneously.

### **Threads**

- A **process** typically has a single thread of execution.
- **Threads** allow a process to have **multiple program counters**, enabling several parts of the program to execute simultaneously.
    - **Multiple threads of control** mean different parts of the program can run independently.
- Each thread requires its own **storage space** for details and program counters, which are managed within the **Process Control Block (PCB)**.

---

### **Final Takeaways**

✔ **Threads** enable a process to execute multiple parts simultaneously.  
✔ Each thread has its own **program counter**, allowing independent execution.  
✔ **PCB** must store details for each thread, including multiple program counters.  
✔ Threads enhance performance by enabling **concurrent execution** within a process.

### **Process Scheduling**

- **Process Scheduler:** Selects among available processes to execute on the CPU core.
- **Goal:** Maximize CPU usage by quickly switching processes onto the CPU core.
- **Scheduling Queues:**
    - **Ready Queue:** Contains all processes in main memory that are ready and waiting to execute.
    - **Wait Queues:** Contains processes waiting for an event (e.g., I/O operations).
- Processes can migrate between different queues during execution.

---

### **Final Takeaways**

✔ The **Process Scheduler** ensures efficient CPU usage by selecting processes for execution.  
✔ **Ready Queue** holds processes ready to run, while **Wait Queues** hold processes waiting for events.  
✔ Processes move between queues depending on their state and system requirements.

### **CPU Switch From Process to Process**

A **context switch** occurs when the CPU switches from executing one process to another. This process ensures that the state of the currently running process is saved so that it can resume execution later, and the state of the next process is loaded into the CPU.

---

### **Process of Context Switching:**

1. **Interrupt or System Call:**
    
    - The CPU receives an interrupt or a system call, signaling the need to switch processes.
2. **Save State into PCB (Process Control Block):**
    
    - The state of the currently executing process (Process P0P_0P0​) is saved into its PCB (PCB0PCB_0PCB0​). This state includes the program counter, registers, and other process information.
3. **Reload State from PCB:**
    
    - The state of the next process (Process P1P_1P1​) is reloaded from its PCB (PCB1PCB_1PCB1​). The CPU resumes execution from where this process was paused.
4. **Execution of New Process:**
    
    - The CPU begins executing the newly loaded process, while the previous process remains idle until it is resumed.

---

### **Key Concepts:**

- **Process State:** The process that is paused is moved to the **idle** state, and the process that is resumed enters the **executing** state.
- **Efficiency:** Context switching introduces overhead because the CPU spends time saving and loading process states instead of executing instructions.
- **Scheduling:** The decision to switch processes is managed by the **process scheduler**, which selects the next process to execute based on scheduling algorithms.

---

### **Final Takeaways:**

✔ **Context switching** allows the CPU to switch between processes, ensuring multitasking.  
✔ The **state** of each process is saved in its **Process Control Block (PCB)**.  
✔ The process being paused moves to the **idle** state, while the process being resumed moves to the **executing** state.  
✔ **Interrupts and system calls** trigger context switches.  
✔ Context switching introduces **overhead**, as it takes time to save and reload states.

### **Context Switch**

When the CPU switches from one process to another, the system must **save the state** of the current process and **load the saved state** of the new process. This process is called a **context switch**.

---

### **Key Points:**

- **Context** refers to the process's state, stored in the **Process Control Block (PCB)**.
- **Context-switch time** is considered **pure overhead** since the system performs no useful work during the switch.
    - **More complex OS and PCB** result in **longer context-switch times**.
- **Hardware support** impacts context-switch time:
    - Some hardware can store **multiple sets of registers** to reduce switch time, allowing **multiple contexts** to be loaded simultaneously.

---

### **Process of a Context Switch:**

1. **Save State:** The CPU saves the current process's state (program counter, registers, etc.) into its **PCB**.
2. **Load State:** The CPU retrieves the next process's state from its **PCB**.
3. **Execution Resumes:** The CPU resumes executing the next process from where it left off.

---

### **Final Takeaways:**

✔ A **context switch** occurs when the CPU switches from one process to another.  
✔ The process's **context** is stored in the **PCB** and reloaded when switching back.  
✔ **Context-switch time** is overhead because no user instructions are executed during the switch.  
✔ **Hardware support** can reduce context-switch time by storing multiple sets of **registers** for faster switching.

### **Multitasking in Mobile Systems**

Mobile operating systems handle multitasking by managing **foreground** and **background** processes, with different capabilities and limitations.

---

### **Key Points:**

- **Early iOS Versions:** Allowed only one process to run at a time, with others suspended.
    
- **Modern iOS:**
    
    - **Foreground Process:** The primary process controlled via the user interface.
    - **Background Processes:** Multiple processes run in memory but are not displayed.
        - Limited to short tasks, event notifications, and long-running tasks like music playback.
- **Android System:**
    
    - Runs both **foreground and background processes** with fewer limitations.
    - **Background Process** uses a **service** to perform tasks.
        - A **service** can continue running even if the background process is suspended.
        - **Service** operates without a user interface and uses minimal memory.

---

### **Final Takeaways:**

✔ **Foreground processes** interact directly with the user.  
✔ **Background processes** run without user interaction, handling tasks like notifications and audio playback.  
✔ **iOS** limits background processes, while **Android** offers more flexibility.  
✔ **Services** in **Android** perform background tasks, using minimal memory and no user interface.

### **Operations on Processes**

#### **Process Creation**

- **Parent Process:** Creates child processes, forming a process tree.
- **Process Identifier (PID):** Each process is identified and managed using a unique PID.
- **Resource Sharing Options:**
    - Parent and child share all resources.
    - Child shares a subset of the parent’s resources.
    - Parent and child share no resources.
- **Execution Options:**
    - Parent and child execute concurrently.
    - Parent waits until children terminate.

---

#### **Process Termination**

- Process executes its last statement and requests termination using the **exit()** system call.
    - **wait()**: Returns the child's status data to the parent.
    - OS deallocates the process's resources.
- Parent can terminate a child using **abort()** if:
    - The child exceeds resource limits.
    - The child's task is no longer needed.
    - The parent exits, and the OS does not allow child continuation.

---

#### **Cascading Termination**

- If a parent process terminates, all its children, grandchildren, etc., are terminated automatically.
- The OS initiates cascading termination.

---

#### **Process States After Termination**

- **Zombie:** Process has terminated, but its parent did not invoke **wait()**.
- **Orphan:** Process continues running after its parent has terminated.

---

### **Final Takeaways**

✔ Processes are created by parent processes, forming a hierarchical tree.  
✔ Resource sharing can be full, partial, or none between parent and child.  
✔ Processes terminate using **exit()**, and parents can wait using **wait()**.  
✔ Cascading termination ensures child processes are terminated if the parent exits.  
✔ **Zombies** occur when no parent waits; **orphans** occur when parents terminate before waiting.

### **Android Process Importance Hierarchy**

1. **Foreground Process**
    
    - Highest priority process, directly interacting with the user.
    - Example: The app currently visible and in use.
2. **Visible Process**
    
    - Partially visible to the user but not in the foreground.
    - Example: A dialog box or notification window.
3. **Service Process**
    
    - Performs background tasks without a user interface.
    - Example: Playing music or syncing data.
4. **Background Process**
    
    - Running but not directly visible or interacting with the user.
    - Example: A messaging app waiting for notifications.
5. **Empty Process**
    
    - Retains app data in memory for faster relaunch but has no active tasks.
    - Example: An app that the user recently closed.

---

### **Process Termination Order**

- Android terminates processes starting from the **least important** (Empty Process) to **most important** (Foreground Process) when reclaiming system resources like memory.
- This ensures the best user experience by preserving critical and interactive processes.

### **Multiprocess Architecture – Chrome Browser**

1. **Single vs. Multiprocess Browsers**
    - Traditional browsers ran as a **single process**, meaning one problematic website could crash the entire browser.
    - **Google Chrome** uses a **multiprocess architecture** to enhance stability, security, and performance.

---

1. **Chrome’s Three Process Types**
    - **Browser Process:**
        
        - Handles the user interface, disk I/O, and network I/O.
        - Manages coordination between different tabs and processes.
    - **Renderer Process:**
        
        - Renders web pages and executes **HTML, JavaScript**, and other web content.
        - Each website opened gets its own renderer process for isolation.
        - Runs in a **sandbox** to limit access to system resources and prevent security exploits.
    - **Plug-in Process:**
        
        - Manages each type of **browser plug-in** (like Flash or PDF readers) independently to prevent crashes from affecting other components.

---

1. **Process Isolation for Stability**
    - Each **tab** in Chrome operates as a **separate process**, ensuring that if one tab crashes, it does not affect the others.
    - This design also enhances **security** by isolating web content from the system.

---

### **Final Takeaways**

✔ Chrome’s **multiprocess architecture** improves stability, performance, and security.  
✔ The **Browser Process** manages overall browser functions and I/O.  
✔ The **Renderer Process** handles web page content, with each tab having its own process.  
✔ The **Plug-in Process** isolates plug-ins, preventing failures from affecting the browser.  
✔ **Sandboxing** restricts renderer processes to limit their system access.

---
## 🗝️ Key Terms

- **Process:** A program in execution that progresses sequentially without parallel instruction execution.
    
- **Text Section:** Part of a process that contains program code.
    
- **Program Counter:** Tracks the current execution position and processor registers.
    
- **Stack:** Stores temporary data such as function parameters, return addresses, and local variables.
    
- **Data Section:** Stores global variables.
    
- **Heap:** Allocates memory dynamically during runtime.
    
- **Process Control Block (PCB):** Stores essential information about each process, including state, program counter, registers, scheduling information, and I/O status.
    
- **Thread:** A sequence of execution within a process, allowing multiple parts of a program to execute simultaneously.
    
- **Process Scheduler:** Selects processes for execution on the CPU core to maximize efficiency.
    
- **Context Switch:** The CPU process of saving and loading the state of processes during switching.
    
- **Foreground Process:** Directly interacts with the user.
    
- **Background Process:** Runs without direct user interaction.
    
- **Zombie Process:** A terminated process whose parent has not invoked wait().
    
- **Orphan Process:** A process that continues running after its parent has terminated.
    
- **Multiprocess Architecture:** A design where each task or tab runs as a separate process (e.g., Google Chrome).
    
- **Sandbox:** A security mechanism that restricts a process’s access to system resources.

---

## 💡 Key Points

**Process Concept:**

- A process is an active execution of a program that consists of components like the text section, program counter, stack, data section, and heap.
    
- A program is passive and becomes a process when loaded into memory.
    

**Process States:**

- **New:** Being created.
    
- **Running:** Actively executed by the CPU.
    
- **Waiting:** Paused, awaiting an external event.
    
- **Ready:** Ready to execute.
    
- **Terminated:** Execution complete.
    

**Process Control Block (PCB):**

- Stores essential process information for management and context switching.
    

**Threads:**

- Multiple threads within a process allow simultaneous execution of different program parts.
    

**Process Scheduling:**

- **Ready Queue:** Processes ready to execute.
    
- **Wait Queues:** Processes waiting for external events.
    

**Context Switch:**

- Saves the current process state and loads the next process state, ensuring multitasking.
    
- Context-switch time is overhead as no user instructions are executed during the switch.
    

**Multitasking in Mobile Systems:**

- **Foreground Process:** Interacts with the user.
    
- **Background Process:** Runs without user interaction.
    
- **Service Process:** Performs background tasks using minimal memory.
    

**Process Operations:**

- **Creation:** Parent processes create child processes.
    
- **Termination:** Uses `exit()` and `abort()` system calls. Cascading termination occurs when a parent process terminates.
    
- **Zombie:** Terminated without a parent invoking `wait()`.
    
- **Orphan:** Continues running after its parent terminates.
    

**Android Process Importance Hierarchy:**

- Order: Foreground > Visible > Service > Background > Empty.
    
- Least important processes are terminated first.
    

**Multiprocess Architecture – Chrome Browser:**

- **Browser Process:** Manages user interface and I/O.
    
- **Renderer Process:** Renders web pages and runs in a **sandbox** for security.
    
- **Plug-in Process:** Handles browser plug-ins.
    
- Each tab runs as a separate process, ensuring stability and security.
    

---

## ✨ Summary

A process is the active execution of a program, consisting of essential components such as the text section, stack, data section, and heap. Processes pass through states like New, Running, Waiting, Ready, and Terminated, with transitions managed by the Process Control Block (PCB). Threads enable concurrent execution within a process, improving performance. The process scheduler ensures efficient CPU usage by managing queues of ready and waiting processes.

Context switching allows the CPU to switch between processes, with overhead time that doesn't execute user instructions. Mobile systems manage processes based on priority, ensuring that foreground processes receive more resources. In Chrome’s multiprocess architecture, each tab and plug-in operates as an isolated process within a sandbox, enhancing stability, performance, and security.

---

## ❓Review Questions

1. **Define a process and list its key components.**
    
2. **Explain the difference between a program and a process.**
    
3. **What are the five states of a process, and how do they transition?**
    
4. **What information is stored in a Process Control Block (PCB)?**
    
5. **What is a thread, and how does it enhance process performance?**
    
6. **Describe the role of the process scheduler and its queues.**
    
7. **What is a context switch, and why is its time considered overhead?**
    
8. **Differentiate between a zombie process and an orphan process.**
    
9. **Explain the Android process importance hierarchy and its impact on resource management.**
    
10. **How does Chrome’s multiprocess architecture improve browser performance and security?**
    
11. **What is a sandbox, and why is it essential for security?**
    
12. **How do parent and child processes share resources, and what are their execution options?**
    
13. **What is cascading termination, and why is it necessary?**