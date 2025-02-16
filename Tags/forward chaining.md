- **Definition**: A data-driven approach where reasoning starts with known facts and applies rules to derive new facts until a goal is reached or no more rules apply.
- **Process**:
    1. Start with a set of **facts** in the knowledge base.
    2. Evaluate the **IF conditions** of rules.
    3. If a rule's conditions are satisfied, execute its **THEN action** to infer a new fact.
    4. Repeat the process with the new fact(s) until the desired goal or conclusion is achieved.
- **Best For**: Situations where all facts are known upfront, and you need to deduce new conclusions (e.g., **diagnostics**, **automation**, **monitoring** systems).
- **Example**:
    - Facts: (1) The car doesn’t start, (2) The fuel gauge is empty.
    - Rule: IF the car doesn’t start AND the fuel gauge is empty THEN fill the gas tank.
    - Conclusion: Fill the gas tank.