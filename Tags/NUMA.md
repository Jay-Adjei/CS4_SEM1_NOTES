### **NUMA** stands for **Non-Uniform Memory Access**.

In a **NUMA** system, a computer has multiple CPUs, each with its own local memory. Unlike traditional systems where all CPUs share the same memory, **NUMA** assigns specific memory to each CPU. This design improves performance because a CPU can access its local memory faster than memory linked to other CPUs.

---

### **Simple Explanation of NUMA-Aware Systems:**

Imagine a library with several librarians, each responsible for a different section of books. If a librarian needs a book from their section, they can get it quickly. But if they need a book from another librarian’s section, it takes longer.

In a **NUMA-aware** system, the operating system ensures that when a CPU runs a program (or thread), it uses the memory closest to that CPU. This reduces the time needed to access data, making the system faster and more efficient.

For example:

- If **CPU 1** is running a program, it will use **Memory 1** located nearby.
- If **CPU 2** runs a different program, it will use **Memory 2** that is close to it.

This design reduces delays because CPUs don’t need to wait for data from distant memory, improving system performance.