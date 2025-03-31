**Definition:**  
A **semaphore** is a synchronization tool used in operating systems to manage access to shared resources by multiple processes or threads.

**Types:**

1. **Counting Semaphore** – Can take non-negative integer values. Used to manage a resource with multiple instances.
    
2. **Binary Semaphore (Mutex)** – Can only be 0 or 1. Used for mutual exclusion (only one thread/process can access a resource at a time).
    

**Operations:**

- **wait(s)** _(also called P or down)_:  
    Decreases the value of semaphore `s`.
    
    - If `s > 0`: process continues.
        
    - If `s = 0`: process is blocked until `s > 0`.
        
- **signal(s)** _(also called V or up)_:  
    Increases the value of semaphore `s` and may unblock a waiting process.
    

**Purpose:**

- Prevents **race conditions**.
    
- Solves **critical section** problems.
    
- Can be used to avoid **deadlocks** if used carefully.