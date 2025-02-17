## **🔒 What is Encryption?**

Encryption is the process of **converting plaintext (readable data) into ciphertext (unreadable format)** to protect it from unauthorized access. Only those with the correct **decryption key** can revert it to its original form.

### **🟢 How Encryption Works (Step-by-Step)**

1. **Plaintext** – The original, readable data.
2. **Encryption Algorithm** – A mathematical formula scrambles the data.
3. **Encryption Key** – A secret key that determines how data is scrambled.
4. **Ciphertext** – The encrypted, unreadable data.
5. **Transmission** – The encrypted data is sent securely over a network.
6. **Decryption Algorithm** – Uses a key to convert ciphertext back into plaintext.
7. **Decrypted Data** – The original message is restored for authorized users.

📌 **Example:**

- **Plaintext:** `HELLO`
- **Encryption Key:** `XYZ123`
- **Ciphertext:** `7F9D@#`
- **Decryption Key:** `XYZ123`
- **Restored Plaintext:** `HELLO`

---

## **🟠 Types of Encryption**

Encryption is broadly classified into **two main types:**

### **1️⃣ Symmetric Encryption (Private Key)**

- Uses **one secret key** for both **encryption and decryption**.
- Faster but less secure for large-scale communication.
- If the key is stolen, all encrypted data is compromised.

**Examples of Symmetric Encryption:** ✅ **AES (Advanced Encryption Standard)** – Used for secure communication and file encryption.  
✅ **DES (Data Encryption Standard)** – Older method, replaced by AES.  
✅ **3DES (Triple DES)** – Enhanced version of DES, more secure but slower.

**📌 Example:**

- Sender and receiver **share the same key** (`12345`).
- **Encrypt:** `HELLO` → `5F8A2`
- **Decrypt:** `5F8A2` → `HELLO`

---

### **2️⃣ Asymmetric Encryption (Public Key)**

- Uses **two keys**:  
    🔑 **Public Key** (used for encryption)  
    🔐 **Private Key** (used for decryption)
- More secure but **slower** than symmetric encryption.
- Used in **secure email, digital signatures, and online banking.**

**Examples of Asymmetric Encryption:** ✅ **RSA (Rivest-Shamir-Adleman)** – Used in SSL/TLS (web security, digital signatures).  
✅ **ECC (Elliptic Curve Cryptography)** – Faster and more efficient than RSA.  
✅ **Diffie-Hellman** – Used for secure key exchange in cryptography.

**📌 Example:**

- Sender encrypts a message using the **receiver’s public key**.
- Receiver decrypts it using their **private key**.
- Even if hackers intercept the public key, they **cannot decrypt the data** without the private key.