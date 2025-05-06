## ✅ **Best Wireless Adapters for WEP/WPA Cracking**

| Adapter Model                 | Chipset           | Monitor Mode     | Packet Injection | Notes                                                                 |
| ----------------------------- | ----------------- | ---------------- | ---------------- | --------------------------------------------------------------------- |
| **ALFA AWUS036NHA**           | Atheros AR9271    | ✅                | ✅                | Gold standard for wireless pentesting (2.4GHz only)                   |
| **ALFA AWUS036NH**            | Ralink RT3070     | ✅                | ✅                | Good signal strength, also 2.4GHz                                     |
| **ALFA AWUS036ACH**           | Realtek RTL8812AU | ✅ (with drivers) | ✅                | Dual-band (2.4GHz + 5GHz), may need driver tweaks on Kali             |
| **Panda PAU06**               | Ralink RT5372     | ✅                | ✅                | Lightweight, low-cost alternative                                     |
| **TP-Link TL-WN722N v1 only** | Atheros AR9271    | ✅                | ✅                | Excellent budget adapter — **avoid v2/v3** (Realtek, no monitor mode) |

---

## 🧪 What to Look for in a Wi-Fi Adapter for Cracking:

* **Supports monitor mode** (aka “promiscuous mode”)
* **Supports packet injection**
* Compatible with **Kali Linux**
* Uses a chipset with **good driver support** (Atheros is best)

---

## ⚠️ Adapter Warning:

* Some models have **multiple versions** — only certain versions support monitor/injection.

  * E.g., **TP-Link TL-WN722N v1** works great, but **v2/v3 DO NOT**.

---

## 🛠️ Check If Your Adapter Works

After plugging in:

```bash
iwconfig
```

Put it in monitor mode:

```bash
airmon-ng start wlan0
```

Test injection:

```bash
aireplay-ng --test wlan0mon
```
