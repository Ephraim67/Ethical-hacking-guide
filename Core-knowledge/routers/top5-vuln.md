# 📈 Top 5 Most Exposed Home IoT Devices on Shodan

---

## 1. **Hikvision CCTV Cameras** 📷

- **Why:**  
  Many Hikvision cameras (and DVR/NVR systems) are **left exposed** on port 80 (HTTP) or 554 (RTSP streaming).
- **Problem:**  
  - Default admin passwords
  - Some firmware has **remote code execution** (RCE) vulnerabilities
- **Shodan search example:**
  ```text
  hikvision port:80
  ```

**⚠️ Real risk:** Some let you watch the live camera feed without logging in!

---

## 2. **Netgear Routers** 📡

- **Why:**  
  Home routers are exposed due to **bad remote management settings** (over ports like 80, 443, 7547).
- **Problem:**  
  - Old firmware has remote takeover vulnerabilities (e.g., authentication bypass)
  - Exposed admin panels
- **Shodan search example:**
  ```text
  netgear port:80
  ```

**⚡ Note:** TR-069 (port 7547) is *very dangerous* when open!

---

## 3. **GoAhead Web Servers (Embedded in Cameras, Baby Monitors, Smart Devices)** 🍼📷

- **Why:**  
  **GoAhead** is a tiny web server embedded in many cheap devices (China-based IP cameras, smart plugs, DVRs).
- **Problem:**  
  - Default creds like `admin:admin`
  - Remote file disclosure and buffer overflow vulnerabilities
- **Shodan search example:**
  ```text
  product:"GoAhead-Webs"
  ```

**👀 Real-world impact:**  
I've seen **baby monitors**, **pet cameras**, and even **kitchen appliances** exposed this way.

---

## 4. **Dahua DVRs and NVRs** 📼

- **Why:**  
  Dahua is a massive CCTV manufacturer, and their recorders (DVR/NVR) are often exposed.
- **Problem:**  
  - CVEs like **CVE-2017-7921** (backdoor accounts)
  - Open telnet/SSH
- **Shodan search example:**
  ```text
  dahua port:37777
  ```

**🔓 Backdoors:**  
Some old Dahua devices have **hardcoded usernames** like `admin:7ujMko0admin` that still work.

---

## 5. **Synology NAS Devices** 📦

- **Why:**  
  Synology NAS systems are for home backups. People expose them so they can access files remotely — but don't configure security properly.
- **Problem:**  
  - Exposed DSM login page
  - Brute-force attacks
  - Ransomware target (NAS ransomware attacks!)
- **Shodan search example:**
  ```text
  port:5000 title:"Synology DiskStation"
  ```

**🔥 Big threat:**  
Synology warns that **thousands of NAS units** are attacked daily just by being online.

---

# 🧨 Visual Summary

| Rank | Device                   | Main Port(s) | Key Issue                  |
|:----:|:-------------------------|:------------:|:----------------------------|
| 1    | Hikvision Cameras         | 80, 554      | Default passwords, RCE      |
| 2    | Netgear Routers           | 80, 443, 7547| Remote takeover             |
| 3    | GoAhead Web Devices       | 80           | Admin panel exposed         |
| 4    | Dahua DVR/NVR             | 37777        | Backdoors, weak security    |
| 5    | Synology NAS              | 5000         | Brute force + ransomware    |

---

# 💬 Final Tips
- If you scan Shodan **today**, you’ll still find **live screenshots** of people's homes, streets, parking lots.
- **Always change default credentials**, **disable UPnP**, **restrict remote access**, and **update firmware**.
- If you see **port 7547** open on a home router — **that’s urgent** — patch or firewall it now.
