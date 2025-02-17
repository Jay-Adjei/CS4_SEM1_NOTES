### **Steps for Odd Parity:**

1. Count the number of `1`s in the given binary data.
2. **If the count is odd**, set the parity bit to **0** (since it's already odd).
3. **If the count is even**, set the parity bit to **1** (to make the total odd).
4. Append the parity bit to the data.

**Example:**

- **Data:** `1010110` (**Four 1s → Even count**)
    
- **Parity Bit:** `1` (Added to make it odd)
    
- **Transmitted Data (with odd parity):** `10101101`
    
- **Data:** `1101001` (**Three 1s → Odd count already**)
    
- **Parity Bit:** `0` (No need to change)
    
- **Transmitted Data (with odd parity):** `11010010`