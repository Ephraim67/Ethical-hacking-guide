- **Shodan** 🔍
- **Qualys SSL Labs** 🛡️
- **Nmap** 🧠


# External Vulnerability Scan on a Home Router


## 1. **Using Shodan** (search engine for Internet-connected devices)

### What it does:
- Shows **open ports**, **services**, **banners**, and **potential vulnerabilities** based on public exposure.

### How to scan:
- First, find your **Public IP**:
  ```bash
  curl ifconfig.me
  ```

- Then, go to [https://www.shodan.io/](https://www.shodan.io)

- In the search bar, type your **public IP address**.

**Example:**  
`Search: 123.45.67.89`

You will see:
- Open ports (e.g., 80, 443, 23, 7547)
- Services (like HTTP, SSH, Telnet)
- Vulnerabilities (sometimes it shows CVEs)
- Potential exposures (e.g., default passwords)

**⚡ Tip:**  
If you make a Shodan account (free), you get more detailed results.

---

## 2. **Using Qualys SSL Labs** (only checks HTTPS services)

### What it does:
- Checks **SSL/TLS security** of your web server (your router must have HTTPS enabled for this to work).
- Looks for:
  - Weak ciphers
  - Bad certificates
  - SSL vulnerabilities (like Heartbleed)

### How to scan:
- Go to [https://www.ssllabs.com/ssltest/](https://www.ssllabs.com/ssltest/)
- Enter your **public IP** (or hostname if you have one).

If your router has a **HTTPS admin page exposed to the internet**, this will test its security.

**⚡ Tip:**  
If you don’t have HTTPS exposed, SSL Labs won't work for your router. (Good thing — admin panels should NOT be exposed publicly!)

---

## 3. **Using Nmap** (manual scanning with your own tools)

You can run an **external Nmap scan** against your public IP address.

**⚠️ Warning:**  
If you scan from *inside your network* against your public IP, you may just hit your internal NAT — so you need to scan **from outside** (like a VPS, cloud machine, or use a VPN that exits elsewhere).

---

### Basic external scan:
```bash
nmap -Pn <your-public-ip>
```
- `-Pn` disables host discovery (assume the target is online)

---

### Scan for common ports and versions:
```bash
nmap -sV -Pn -T4 <your-public-ip>
```
- `-sV` = service version detection
- `-T4` = faster scan

---

### Scan for vulnerabilities (requires Nmap scripts):
```bash
nmap --script vuln -Pn <your-public-ip>
```
- This will run vulnerability scripts (like checking for old SSL, SMB vulnerabilities, etc.)

---

### Example full command for a serious check:
```bash
nmap -sS -sV --script vuln -O -Pn <your-public-ip>
```
- `-sS` = stealthy SYN scan
- `-O` = OS detection

---

# 🚨 Important Things to Know
- If **no ports** are open to the internet on your router, that’s **good**.
- If you see **Telnet**, **FTP**, **SSH**, **UPnP**, **HTTP Admin**, or **Remote Management Ports** open — you should **disable** them immediately unless absolutely needed.
- Always **update your router firmware** after scans — it might fix vulnerabilities.
- **Disable remote administration** unless you 100% need it.
- **Use strong passwords** and **multi-factor authentication** (if router supports it).

---

# 📋 Quick Summary Table

| Tool          | Purpose                                       | Risk Level      |
|---------------|------------------------------------------------|-----------------|
| **Shodan**    | Public exposure and open services             | Very safe       |
| **SSL Labs**  | HTTPS encryption weakness check               | Very safe       |
| **Nmap**      | Custom manual vulnerability scan              | Be careful with aggressive scans |

---

# ⚙️ Want me to also show you:
- How to **harden your router** after finding vulnerabilities? 🔥
- OR a **bash script** that runs Nmap and formats the result nicely?
