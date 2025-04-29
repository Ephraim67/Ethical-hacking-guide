- **CCTV cameras** 📷
- **Smart TVs**
- **Baby monitors**
- **IoT devices** (like printers, fridges, speakers)
- **Routers, NAS, etc.**


# 🔥 How to Use Shodan to Identify Exposed Home Devices

---

## 1. **Set up a free Shodan account**

Go to: [https://account.shodan.io/register](https://account.shodan.io/register)

- You’ll need an account for **full search power** (filters, download results, more pages).

---

## 2. **Learn Shodan search basics**

Shodan works by **searching service banners** — it looks at the info devices leak when they are online.

You search by **keywords**, **port numbers**, **device type**, or **organization**.

---

## 3. **Useful Shodan search filters**

| Filter | Meaning |
|:------|:--------|
| `port:` | Search by open port |
| `country:` | Search by country |
| `org:` | Search by ISP or company |
| `net:` | Search by IP range |
| `os:` | Search by operating system |
| `product:` | Search by product name |
| `title:` | Search by web page title |
| `vuln:` | Search by known CVEs |

---

## 4. **Specific Shodan searches for home gadgets**

Here are some **killer search examples**:

### 🎥 Exposed CCTV Cameras
```text
port:554 has_screenshot:true
```
- Port 554 = RTSP stream (Real-Time Streaming Protocol, often cameras).

Or more direct:
```text
webcamXP
```
(looks for popular webcam software)

Or:
```text
port:80 title:"DVR Login"
```
(lots of CCTV Digital Video Recorders (DVRs) use this title)

---

### 🛜 Generic Home Routers
```text
netgear port:80
tplink port:80
linksys port:80
```
or
```text
port:7547
```
(TR-069 — remote management service for many routers — often dangerously exposed!)

---

### 🖨️ Printers, NAS, Smart Devices
```text
port:9100
```
(HP JetDirect printers — can be abused for printing garbage or DoS)

```text
port:5000 title:"Synology"
```
(Synology NAS storage boxes)

```text
port:37777
```
(Common DVR TCP port for CCTV systems)

---

### 👶 Baby Monitors, Smart Cameras
```text
product:"GoAhead-Webs"
```
(used in many cheap baby monitors and cameras)

```text
title:"IP Camera"
```
(simple, finds open webcams)

---

## 5. **Hunt by Device Manufacturer**
If you know popular brands:
```text
hikvision
dahua
axis
arlo
wyze
```
- These are major CCTV/baby cam manufacturers.

---

## 6. **Extra: Add location to narrow it down**
Example to find **open cameras in the US**:
```text
port:554 country:"US"
```

Example to find **TP-Link routers in Germany**:
```text
tplink country:"DE"
```

---

# 🚨 Important Notes
- Many devices **should not** be exposed publicly.
- Some cameras **don't even require passwords** (anonymous access).
- **Accessing without permission is illegal** — scanning/searching is OK, but don't try to log in unless it's your own device or you have permission.

If you are scanning your own home:
- Find out if **your camera is exposed**.
- If yes: **close the port**, **disable UPnP**, **set a strong password**, **update firmware**.

---

# 🧠 Example Practical Exercise

Imagine you want to find unsecured webcams around the world:
```text
port:554 has_screenshot:true
```

You'll see **live screenshots** from cameras (street cams, parking lots, houses, stores) — scary but educational.

---

# 🛠️ Bonus Tools

If you want to **automate Shodan scanning**, you can use the **Shodan CLI**:

Install:
```bash
pip install shodan
```

Initialize:
```bash
shodan init YOUR_API_KEY
```

Scan:
```bash
shodan search 'port:554 has_screenshot:true'
```

(You need a free Shodan API key from your account.)

---

# ⚡ Quick Cheat Sheet

| Task                          | Shodan Command                         |
|:-------------------------------|:---------------------------------------|
| Find exposed webcams           | `port:554 has_screenshot:true`          |
| Find routers                   | `netgear port:80`, `tplink port:80`    |
| Find smart devices             | `product:"GoAhead-Webs"`               |
| Search by country              | `port:554 country:"US"`                 |
| Narrow by brand                | `hikvision`, `dahua`, `arlo`           |

---

# Final Pro Tip
If you see devices exposed, the **three main mistakes** are usually:
- Weak or no password
- Open management ports (HTTP, SSH, Telnet)
- Automatic port forwarding (UPnP)

Always **harden** your devices after scanning!
