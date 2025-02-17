### **Steps for Even Parity:**

1. Count the number of `1`s in the given binary data.
2. **If the count is even**, set the parity bit to **0**.
3. **If the count is odd**, set the parity bit to **1** (to make the total even).
4. Append the parity bit to the data.

**Example:**

- **Data:** `1010110` (**Four 1s → Even count already**)
    
- **Parity Bit:** `0` (No need to change)
    
- **Transmitted Data (with even parity):** `10101100`
    
- **Data:** `1101001` (**Three 1s → Odd count**)
    
- **Parity Bit:** `1` (Added to make it even)
    
- **Transmitted Data (with even parity):** `11010011`