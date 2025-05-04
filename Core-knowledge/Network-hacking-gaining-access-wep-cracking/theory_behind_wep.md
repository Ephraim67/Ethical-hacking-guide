### 🔓 Theory Behind Cracking WEP Encryption

**WEP (Wired Equivalent Privacy)** is an obsolete and insecure Wi-Fi security protocol. It was designed to provide wireless security comparable to a wired network but has major flaws in its implementation—making it highly vulnerable to cracking. Here's the theoretical foundation of how WEP can be broken:

---

### 🔹 1. **WEP Basics**

* **Encryption Algorithm**: WEP uses **RC4 stream cipher** for encryption.
* **Key Size**: Typically 40-bit or 104-bit secret key + 24-bit Initialization Vector (IV) = 64-bit or 128-bit total.
* **Data Encryption Process**:

  * WEP uses a shared secret key.
  * A 24-bit IV is prepended to the key.
  * IV + secret key = RC4 key → used to generate a keystream.
  * This keystream is XORed with the plaintext to produce ciphertext.

---

### 🔹 2. **WEP Vulnerabilities**

#### ❌ Weak IVs (Initialization Vectors)

* IVs are only 24 bits long → **only \~16 million combinations**.
* IVs are transmitted in plaintext with each packet.
* IV reuse is frequent, especially on busy networks.

#### ❌ RC4 Key Scheduling Weakness

* Some IVs are **"weak"** and leak information about the secret key when used with RC4.
* Fluhrer, Mantin, and Shamir (FMS attack) showed that **analyzing these weak IVs reveals key bytes over time**.

---

### 🔹 3. **Cracking Methodology**

Here’s how attackers exploit these weaknesses:

#### Step 1: **Packet Capture**

* Use tools like `airodump-ng` to collect a large number of packets from the target network.
* Focus on **ARP packets** because they're small and predictable (easy to guess plaintext).

#### Step 2: **Inject Traffic (Optional)**

* Use `aireplay-ng` to **inject ARP requests** to generate more encrypted traffic and IVs quickly.
* This speeds up the capture process significantly.

#### Step 3: **Collect IVs**

* Store the IVs from captured packets. Thousands to millions may be needed.

#### Step 4: **Key Cracking**

* Use tools like `aircrack-ng` to analyze the IVs and **apply statistical analysis** (e.g., FMS, KoreK, PTW attacks).
* These attacks guess key bytes based on IV patterns and eventually recover the WEP key.

---

### 🔹 4. **Cracking Tools**

* `aircrack-ng`: De facto suite for WEP/WPA cracking.
* `airodump-ng`: Packet capture tool.
* `aireplay-ng`: Traffic injection tool.

---

### 🔹 5. **Why WEP Is Broken**

* **Short IV** + **plaintext IV transmission** + **RC4 flaws** + **poor key management** = Cracked in minutes.
* It was replaced by **WPA/WPA2**, which fix many of these issues.
