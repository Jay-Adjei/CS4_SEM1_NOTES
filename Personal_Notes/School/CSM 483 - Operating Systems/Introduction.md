---
course:
  - CSM 483
tags: 
last topic: I/O Structure
next topic: I/O Structure (cont.)
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

## Key Points
- Operating system is resource allocator and a control program making efficient use of hardware, and managing execution of user programs.
- The one program that runs at all times is the **kernel**, everything else is either a system program or an application program.
- OSes also include **middleware**, this is a set software frameworks that provide additional services to application developers such as databases, multimedia, and graphics.

## Summary

-