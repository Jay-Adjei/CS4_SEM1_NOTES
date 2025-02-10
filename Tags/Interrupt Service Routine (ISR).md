**Interrupt Service Routines (ISRs)**, also known as **interrupt handlers**, are special functions or routines in a computer system that are executed in response to an interrupt.

### Key Features of ISRs:

1. **Purpose**: They handle specific tasks triggered by interrupts, such as responding to hardware signals or software events.
2. **Execution**:
    - When an interrupt occurs, the CPU stops its current task.
    - It jumps to the appropriate ISR (determined by the **interrupt vector**) to handle the interrupt.
    - After completing the ISR, the CPU resumes the interrupted task.
3. **Tasks Performed**:
    - Processing input/output (e.g., reading data from a keyboard or disk).
    - Handling errors or exceptions (e.g., divide-by-zero errors).
    - Updating system states (e.g., marking a task as complete).
4. **Efficiency**: ISRs are designed to be quick and efficient, as they temporarily pause other operations.

### Example:

If a keyboard key is pressed, an interrupt is generated. The ISR for the keyboard reads the keypress data and processes it, such as displaying the corresponding character on the screen.