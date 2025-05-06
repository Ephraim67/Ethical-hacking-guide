### Bettercap Basics: What It Is & What It Can Do

**Bettercap** is a powerful, modular, and user-friendly tool designed for **network attacks and monitoring**, including **Man-in-the-Middle (MitM)**, **packet sniffing**, **credential harvesting**, and more. It’s a **successor to Ettercap**, written in Go, and supports **interactive CLI scripting**, making it ideal for red teamers and pentesters.


## What Is Bettercap Used For?

| Category                      | Use Case                                                             |
| ----------------------------- | -------------------------------------------------------------------- |
| **Sniffing**               | Capture credentials, HTTP requests, DNS queries, cookies, forms      |
| **Man-in-the-Middle**  | Intercept and manipulate traffic with ARP spoofing or DHCP spoofing  |
| **Network Reconnaissance** | Discover live hosts, scan ports, detect services                     |
| **DNS/HTTPS Hijacking**    | Redirect DNS queries to malicious sites, attempt SSL stripping       |
| **Credential Harvesting**  | Extract HTTP/FTP/SMTP/POP3 creds, cookies, tokens                    |
| **Wi-Fi Attacks**          | Deauth clients, rogue AP, probe sniffing (if using wireless adapter) |
| **Scriptable Automation**  | Custom attack modules via `caplets` (Bettercap scripts)              |



## Key Bettercap Features

### 1. **ARP Spoofing**

```bash
set arp.spoof.targets 192.168.1.100
arp.spoof on
```

### 2. **Sniffing**

```bash
net.sniff on
```

Add `set net.sniff.verbose true` to see full packets.

### 3. **DNS Spoofing**

```bash
dns.spoof on
set dns.spoof.domains example.com
set dns.spoof.address 192.168.1.99
```

### 4. **HTTPS Downgrade (SSLstrip)**

```bash
https.proxy on
https.strip on
```

> Note: Modern browsers with HSTS will block this, making it less effective.

### 5. **Caplets**

Caplets are Bettercap’s automation scripts (like mini scripts for attacks).

Example:

```bash
bettercap -caplet http-cred-sniffer.cap
```

### 6. **Wi-Fi Attacks** (if wireless card supports monitor mode)

```bash
wifi.recon on
wifi.ap on
wifi.deauth all
```

---

## Example: Full ARP Spoofing + Sniffing Setup

```bash
sudo bettercap -iface eth0
```

To check the help page of a module in bettercap:
```bash
help module_name

net.probe on
net.probe off
```

Inside interactive shell:

```bash
set arp.spoof.targets 192.168.1.100
arp.spoof on
net.sniff on
```



## Learn Caplets

```bash
caplets.update
caplets.show
```


* Use in **lab environments** or **with explicit permission** only.
* Some features require **root privileges** and specific **network interfaces** (e.g., `wlan0mon`).
* Combine with tools like `Wireshark`, `mitmproxy`, or `Burp Suite` for deeper analysis.
