---
course:
  - CSM 483
status: Incomplete
last topic: 
next topic:
---

2025-03-31 10:26

# Deadlocks

## 📚Detailed Notes

## **System Model in Operating Systems**

### **Definition:**

- A system consists of _resources_ needed by processes to run.
    
- Resource types include: `R₁, R₂, ..., Rₘ` (e.g., CPU cycles, memory space, I/O devices).
    

### **Instances:**

- Each resource type `Rᵢ` has `Wᵢ` instances available.
    

### **Process Behavior with Resources:**

- A process interacts with a resource in 3 steps:
    
    1. **Request** – the process asks for the resource.
        
    2. **Use** – the process utilizes the resource.
        
    3. **Release** – the process gives up the resource.
        

---

## **Deadlock with [[Semaphores]]**

### **Definition:**

- A deadlock can occur when two threads wait on each other’s resources.
    

### **Setup:**

- Semaphores: `s₁` and `s₂`, both initialized to 1.
    
- Threads: `T₁` and `T₂`.
    

### **Execution Order:**

- `T₁`: `wait(s₁)` → `wait(s₂)`
    
- `T₂`: `wait(s₂)` → `wait(s₁)`
    

### **Result:**

- Both threads end up waiting for the other to release a semaphore → **deadlock**.
    

---

## **Deadlock Characterization**

### **Conditions for Deadlock:**

1. **Mutual Exclusion** – Only one thread can use a resource at a time.
    
2. **Hold and Wait** – A thread holds one resource and waits for another.
    
3. **No Preemption** – A resource cannot be forcibly taken away.
    
4. **Circular Wait** – A cycle exists where each thread waits for a resource held by the next.
    

---

## **Resource-Allocation Graph**

### **Definition:**

- A graphical way to model resource usage.
    

### **Components:**

- **Vertices (V)**: Threads (`T₁, T₂, ..., Tₙ`) and Resources (`R₁, R₂, ..., Rₘ`).
    
- **Edges (E)**:
    
    - **Request edge**: `Tᵢ → Rⱼ` (thread requests resource).
        
    - **Assignment edge**: `Rⱼ → Tᵢ` (resource assigned to thread).
        

---

## **Resource Allocation Graph Example**

### **Scenario:**

- Resources:
    
    - `R₁`: 1 instance
        
    - `R₂`: 2 instances
        
    - `R₃`: 1 instance
        
    - `R₄`: 3 instances
        

### **Threads:**

- `T₁`: Holds `R₂`, waiting for `R₁`.
    
- `T₂`: Holds `R₁` and `R₂`, waiting for `R₃`.
    
- `T₃`: Holds `R₃`.
    

### **Outcome:**

- Graph shows resource holding and waiting relationships visually.
    

---

## **Resource Allocation Graph with a Deadlock**

![[Pasted image 20250331105735.png]]
### **Visual:**

- A cycle in the graph shows that `T₁`, `T₂`, and `T₃` are all waiting in a loop with no one able to proceed.
    

### **Conclusion:**

- Cycle **and** each resource in the cycle has only one instance → **deadlock exists**.
    

---

## **Graph with a Cycle But No Deadlock**

![[Pasted image 20250331105753.png]]
### **Visual:**

- A cycle exists but some resources have **multiple instances** or are not fully occupied.
    

### **Conclusion:**

- **Cycle exists** ≠ **deadlock**.
    
- Deadlock only occurs if the cycle involves resources with **only one instance**.
    

---

## **Final Takeaways** 
✔ A process uses resources in request → use → release order.  
✔ Deadlock occurs when four specific conditions hold simultaneously.  
✔ Semaphores can cause deadlock if not handled carefully.  
✔ Resource Allocation Graphs help visualize and detect potential deadlocks.  
✔ Not all cycles in a graph mean deadlock – resource instances matter.

---

## **Basic Facts About Deadlock**

**If no cycle in graph:**  
➡ No deadlock.

**If cycle exists:**

- If **only one instance** per resource → **Deadlock guaranteed**.
    
- If **multiple instances** per resource → **Deadlock is possible**, but not certain.
    

---

## **Methods for Handling Deadlocks**

**Three main approaches:**

1. **Avoid deadlock entirely:**
    
    - **Deadlock Prevention**
        
    - **Deadlock Avoidance**
        
2. **Let deadlock happen, then recover.**
    
3. **Ignore the problem:**
    
    - Assume deadlock will never happen (used in many real systems).
        

---

## **Deadlock Prevention**

**Idea:** Break one of the **four deadlock conditions** so deadlock can’t happen.

#### 1. **Mutual Exclusion**

- Allow sharing when possible (e.g., read-only files).
    
- Still needed for non-shareable resources.
    

#### 2. **Hold and Wait**

- Don't let threads hold one resource while waiting for another.
    
- Solutions:
    
    - Ask for all resources at once.
        
    - Only request when holding **nothing**.
        
- ⚠️ Leads to **low resource use** and **starvation**.
    

#### 3. **No Preemption**

- If a process can’t get all it needs, take away what it’s holding.
    
- Put those resources back into the pool.
    
- Restart the process later when everything is available.
    

#### 4. **Circular Wait**

- Give each resource a number.
    
- Threads must request resources **in order** (e.g., always ask for 1 before 5).
    
- Prevents loops.
    

---

## **Circular Wait Prevention (in Detail)**

- Each resource (lock) has a number.
    
- Threads must **acquire in increasing order**.
    

**Example:**

- If `first_mutex = 1` and `second_mutex = 5`  
    ➤ `thread_two` cannot lock `second_mutex` before `first_mutex`.
    

➡ This avoids circular wait and prevents deadlock.

---

## **Deadlock Avoidance**

**Idea:** Use extra info to **avoid** entering a dangerous state.

- Each thread tells the system **maximum resources** it may need.
    
- The system checks if granting a request keeps it in a **safe state** (no circular wait).
    
- Resources are given only if it's safe to do so.
    

**Key Concept:**

- System always checks its **resource state** before giving resources.
    

---

## **Final Takeaways**

✔ No cycle → No deadlock.  
✔ Cycle + one instance per resource → Deadlock.  
✔ Multiple strategies exist: prevent, avoid, recover, or ignore.  
✔ Prevention blocks deadlock by breaking key conditions.  
✔ Avoidance uses info to stay in safe zones.  
✔ Circular wait can be stopped with resource ordering.

---

### 🔷 What Is Deadlock Avoidance?

**Deadlock avoidance** is a technique used by the operating system to ensure the system **never enters a state** where deadlock can happen.

🧠 **Key Idea:**  
Before giving a resource to a thread, the system checks if it will **still be able to finish all processes later**. If yes → grant it. If no → make it wait.

---

### 🔷 What Is a Safe State?

A system is in a **safe state** if there is **some order** in which all threads can finish, one after another.

**Safe State = No Deadlock**

#### How It Works:

- There exists a sequence `<T₁, T₂, ..., Tₙ>` such that:
    
    - Each thread **can eventually get the resources it needs**.
        
    - Once it finishes, it releases its resources for the next thread.
        

If the system **can’t guarantee** this, it’s in an **unsafe state**, which **may lead to deadlock**.

---

### 🔷 Safe vs. Unsafe vs. Deadlock (Visual Concept)

From the visual:

- ✅ **Safe State** = No risk of deadlock.
    
- ⚠️ **Unsafe State** = Risk of deadlock, not guaranteed.
    
- ❌ **Deadlock State** = Deadlock has already occurred.
    

**Avoidance = Stay in the safe zone.**

---

### 🔷 Deadlock Avoidance Algorithms

#### 1. **Single Resource Instance**

- Use a **Resource-Allocation Graph**.
    
- Before granting a resource, check if adding the request creates a **cycle**.
    
- If it **does create a cycle** → **don’t grant** the request.
    

#### 2. **Multiple Resource Instances**

- Use the **Banker’s Algorithm** (most common).
    
- Each thread tells the system the **maximum** number of each resource type it might need.
    
- The system:
    
    - Simulates the allocation.
        
    - Checks if it stays in a **safe state**.
        
    - If safe → grant it.
        
    - If unsafe → deny it for now.
        

---

### 🔷 Resource Allocation Graph Scheme (for Single Resource Instance)

- **Claim Edge (dashed)**: Process _may_ request this resource in the future.
    
- **Request Edge**: Process _is currently_ requesting the resource.
    
- **Assignment Edge**: Resource is assigned to the process.
    

➡ If granting a request **forms a cycle** → it’s unsafe → don’t allow it.

---

### 🔷 Unsafe State in the Graph

In the unsafe state image:

- One process (e.g. `T₁`) is **requesting** a resource that another process (`T₂`) is **holding**.
    
- If both continue requesting each other’s resources, it could lead to **deadlock**.
    

---

### 🔷 Resource-Allocation Graph vs. Wait-for Graph

- The **Resource-Allocation Graph** includes both threads and resources.
    
- The **Wait-for Graph** simplifies this by only showing which thread is waiting on which.
    

If the **Wait-for Graph contains a cycle**, that means **deadlock**.

---

### 🔷 Final Takeaways

✔ Deadlock avoidance checks if a system stays in a **safe state** before granting resources.  
✔ **Safe State**: A way to finish all processes without getting stuck.  
✔ **Avoidance** ≠ Prevention — it doesn’t break conditions but instead **avoids dangerous situations**.  
✔ Uses **Resource-Allocation Graph** (1 instance) or **Banker’s Algorithm** (multiple instances).  
✔ Always aim to **avoid unsafe states** to stay deadlock-free.

---

### 🔷 **Resource-Allocation Graph Algorithm (Deadlock Avoidance – Single Instance)**

**How it works:**

- When a thread `Tᵢ` requests a resource `Rⱼ`:
    
    - The system checks if adding a **request edge → assignment edge** will form a **cycle** in the graph.
        
    - **If no cycle** → Grant the resource (safe).
        
    - **If cycle** → Do not grant it (unsafe → risk of deadlock).
        

This only works well when each resource type has **only one instance**.

---

### 🔷 **Resource-Allocation Graph vs. Wait-for Graph**

- **Resource-Allocation Graph** includes:
    
    - Threads (`T₁`, `T₂`, ...)
        
    - Resources (`R₁`, `R₂`, ...)
        
    - Edges show who is **holding** or **requesting** what.
        
- **Wait-for Graph**:
    
    - A simplified version that only includes **threads**.
        
    - Shows which thread is **waiting for another** to release a resource.
        

💡 **If the wait-for graph has a cycle → Deadlock exists.**

---

### 🔷 Recovery from Deadlock: **Process Termination**

**Two options:**

1. **Abort all deadlocked processes** — quick but harsh.
    
2. **Abort one at a time** until deadlock is resolved.
    

**How to choose which thread to abort? Consider:**

1. Priority of the thread.
    
2. How much work it has already done.
    
3. Resources it’s holding.
    
4. Resources it still needs.
    
5. Total number of processes that would need to be aborted.
    
6. Type of process (interactive or batch).
    

---

### 🔷 Recovery from Deadlock: **Resource Preemption**

Instead of killing processes, take their resources.

**Steps:**

1. **Select a victim** (a process to lose its resources):
    
    - Try to pick the one with **least impact**.
        
2. **Rollback**:
    
    - Undo the victim’s progress and return to a **safe state**.
        
3. **Handle starvation**:
    
    - Ensure the same process isn't always picked.
        
    - Use a counter or cost function to avoid unfairness.
        

---

### 🔚 Final Takeaways

✔ The Resource-Allocation Graph Algorithm avoids deadlock by **detecting potential cycles**.  
✔ Wait-for graphs make it easier to see **which threads are blocking others**.  
✔ Recovery can be done by **terminating processes** or **preempting resources**.  
✔ Recovery must be handled carefully to avoid **starvation** or major performance issues.
## 🗝️ Key Terms

| **Term**                      | **Definition**                                                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Deadlock**                  | A situation where a group of processes are stuck waiting for each other’s resources, and none can proceed.                      |
| **Resource-Allocation Graph** | A graphical representation of processes and the resources they request or hold, used to detect deadlocks.                       |
| **Wait-for Graph**            | A simplified version of a resource-allocation graph that only includes processes and shows which process is waiting on another. |
| **Semaphore**                 | A synchronization tool used to manage access to shared resources, often used in thread coordination.                            |
| **Safe State**                | A state where the system can allocate resources to all processes in some order without causing a deadlock.                      |
| **Unsafe State**              | A state that might lead to deadlock; not guaranteed but risky.                                                                  |
| **Circular Wait**             | A condition where processes are waiting on each other in a loop, forming a cycle.                                               |
| **Hold and Wait**             | A condition where a process is holding at least one resource and waiting for others.                                            |
| **Mutual Exclusion**          | A condition where only one process can use a resource at a time.                                                                |
| **No Preemption**             | A condition where resources cannot be forcibly taken from a process—they must be released voluntarily.                          |
| **Claim Edge**                | A dashed line in a resource graph indicating that a process may request a resource in the future.                               |
| **Request Edge**              | A solid arrow from a process to a resource, showing the process is currently requesting it.                                     |
| **Assignment Edge**           | A solid arrow from a resource to a process, indicating the resource is currently assigned.                                      |
| **Banker’s Algorithm**        | A deadlock avoidance algorithm that ensures a system stays in a safe state by simulating allocations.                           |
| **Process Termination**       | A deadlock recovery method where one or more processes are aborted to break the cycle.                                          |
| **Resource Preemption**       | A deadlock recovery method where resources are taken away from a process and given to others.                                   |
| **Starvation**                | A condition where a process never gets the resources it needs because others keep getting picked first.                         |

---
## 💡 Key Points
### 🔹 **System Model**

- Processes need resources like CPU, memory, I/O devices.
    
- Interaction with a resource follows: **Request → Use → Release**.
    
- Each resource type may have multiple instances.
    

### 🔹 **Deadlock**

- Occurs when processes wait on each other in a cycle.
    
- All 4 conditions must hold:
    
    1. Mutual Exclusion
        
    2. Hold and Wait
        
    3. No Preemption
        
    4. Circular Wait
        

### 🔹 **Semaphores and Deadlock**

- Deadlocks can occur when semaphores are used in different orders by threads.
    

### 🔹 **Resource-Allocation Graph**

- Shows which process holds or requests which resource.
    
- A **cycle** in the graph may indicate deadlock (if only one instance of each resource exists).
    

### 🔹 **Safe, Unsafe, Deadlock States**

- **Safe state**: System can complete all processes.
    
- **Unsafe state**: Risk of deadlock.
    
- **Deadlock state**: No progress possible.
    

### 🔹 **Deadlock Prevention**

- Break one of the four necessary conditions:
    
    - Allow sharing (break mutual exclusion)
        
    - Request all resources at once (break hold and wait)
        
    - Preempt resources (break no preemption)
        
    - Order resource requests (break circular wait)
        

### 🔹 **Deadlock Avoidance**

- System avoids deadlock by ensuring it stays in a **safe state**.
    
- Requires knowing the **maximum resource need** in advance.
    
- Uses **Banker’s Algorithm** or **Resource-Allocation Graph Algorithm**.
    

### 🔹 **Recovery Techniques**

#### 1. **Process Termination**

- Abort one or more threads to break the cycle.
    
- Choose based on priority, progress, resource use, etc.
    

#### 2. **Resource Preemption**

- Take resources from one process (victim).
    
- Use rollback to undo its progress.
    
- Prevent starvation by tracking how often a thread is chosen.
---
## ✨ Summary
**Deadlocks** are a critical concept in operating systems, describing a condition where two or more processes are stuck indefinitely, each waiting for resources held by the other. These situations arise when four conditions hold simultaneously: mutual exclusion, hold and wait, no preemption, and circular wait. To model and understand deadlocks, systems use _Resource-Allocation Graphs_ and _Wait-for Graphs_, which visually represent the relationships between threads and the resources they request or hold. A cycle in such graphs, especially when each resource has only one instance, is a strong indicator of deadlock.

To prevent or handle deadlocks, systems adopt various strategies. _Deadlock prevention_ breaks at least one of the four conditions—by allowing shared resources, requiring all resources to be requested at once, enabling preemption, or enforcing a strict order of resource acquisition. _Deadlock avoidance_, on the other hand, ensures the system remains in a _safe state_ by carefully evaluating each resource request. This is often implemented through the _Banker’s Algorithm_ or Resource-Allocation Graph checks. A safe state guarantees that every process can eventually complete; an unsafe state may lead to deadlock.

When deadlocks do occur, systems can recover either by _terminating processes_—based on priority, progress, or resource use—or by _preempting resources_ from selected processes, potentially rolling them back to previous states. While effective, recovery must account for fairness to prevent _starvation_, where a process is repeatedly delayed.

Deadlock handling is vital for ensuring reliability, efficiency, and fairness in multitasking systems. By using visual models, strategic prevention, intelligent avoidance, and controlled recovery, operating systems can maintain smooth process execution and resource management.

---
## ❓Review Questions
- Define **deadlock**. What are the **four necessary conditions** for deadlock to occur?
    
- What is the difference between a **safe state** and an **unsafe state**?
    
- How does a **resource-allocation graph** help detect deadlock?
    
- Explain how **semaphores** can lead to deadlock.
    
- How can **circular wait** be prevented in deadlock prevention?
    
- What information does the **Banker’s Algorithm** require?
    
- Compare **deadlock prevention** and **deadlock avoidance**.
    
- What is **rollback** in the context of deadlock recovery?
    
- List three criteria to choose a process for **termination** during deadlock recovery.
    
- How does the system decide whether to **grant a resource request** in deadlock avoidance?