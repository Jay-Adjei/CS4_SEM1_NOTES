- **Definition**: A goal-driven approach where reasoning starts with a desired goal and works backward to determine what facts or conditions must be true to satisfy the goal.
- **Process**:
    1. Start with a **goal** or hypothesis.
    2. Look for rules where the goal matches the **THEN part**.
    3. Check if the **IF conditions** of those rules are true:
        - If true, the rule is satisfied, and the goal is achieved.
        - If not, the system recursively works backward to prove the conditions of the rule by finding additional facts or rules.
    4. Continue until the goal is proven or no more rules apply.
- **Best For**: Situations where you need to verify or achieve a specific goal (e.g., **consultation systems**, **troubleshooting**, **medical diagnosis**).
- **Example**:
    - Goal: Diagnose a patient with a specific illness.
    - Rule: IF the patient has a fever AND a rash THEN they may have measles.
    - Backward chaining will ask: "Does the patient have a fever?" and "Does the patient have a rash?" to confirm the goal.