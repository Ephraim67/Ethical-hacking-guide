# **Module Topic: Firewalls, VPNs, Proxies, IDS/IPS**


## **In-Depth Explanation**

### **Firewalls**
- **Function**: Control incoming/outgoing traffic based on rules.
- **Types**:
  - **Stateless**: Filters based on static rules (e.g., IP, port).
  - **Stateful**: Tracks session state (e.g., TCP handshakes).
  - **NGFW (Next-Gen Firewall)**: Adds Deep Packet Inspection, App control, and IPS features.



### **VPNs (Virtual Private Networks)**
- **Function**: Securely tunnels data over untrusted networks (like the Internet).
- **Common Protocols**:
  - **OpenVPN** (TLS-based, flexible)
  - **IPSec** (built into most OSes)
  - **WireGuard** (lightweight and fast)
- **Use Case**: Secure remote access or connecting branch offices.

---

### 🌐 **Proxies**
- **Forward Proxy**: Sits between user and internet. Hides the **client** (e.g., anonymous browsing).
- **Reverse Proxy**: Sits in front of a server, hides the **server**. Used for load balancing, caching, TLS termination.
- **Common Tools**: Squid, NGINX, HAProxy

---

### 🛡 **IDS / IPS**
- **IDS (Intrusion Detection System)**:
  - **Monitors** network traffic for known attack patterns.
  - **Example tools**: Snort, Suricata.
- **IPS (Intrusion Prevention System)**:
  - Same as IDS, but it can **block** malicious traffic automatically.

---

## 💡 Lab Project Ideas

---

### 🔧 **Lab 1: Firewall Configuration with pfSense or iptables**

#### ✅ Objective:
Configure a firewall to **allow only HTTP/HTTPS** and **block everything else**.

#### 🛠 Tools:
- pfSense in VirtualBox/VMware **OR** Linux VM with `iptables`
- A browser or CLI tools (`curl`, `ping`, `nmap`)

---

### 🔄 Steps (iptables example):
1. **Flush existing rules**:
   ```bash
   sudo iptables -F
   ```

2. **Set default to DROP all**:
   ```bash
   sudo iptables -P INPUT DROP
   sudo iptables -P FORWARD DROP
   sudo iptables -P OUTPUT DROP
   ```

3. **Allow HTTP (80) & HTTPS (443)**:
   ```bash
   sudo iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT
   sudo iptables -A OUTPUT -p tcp --dport 443 -j ACCEPT
   ```

4. **Test**:
   - Visit websites in a browser: ✅
   - Try `ping google.com`: ❌ (should be blocked)
   - Try `curl http://example.com`: ✅

5. **Log blocked packets** (optional):
   ```bash
   sudo iptables -A OUTPUT -j LOG
   ```

---

### 🧪 **Lab 2: VPN Configuration with OpenVPN**

#### ✅ Objective:
Set up a VPN and compare encrypted vs unencrypted traffic.

#### 🛠 Tools:
- Two VMs or devices
- OpenVPN installed (or use [TryHackMe VPN Labs] or [VPNBook configs])
- Wireshark

---

### 🔄 Steps:
1. **Install OpenVPN**:
   ```bash
   sudo apt install openvpn
   ```

2. **Download free config** (from vpnbook.com):
   ```bash
   sudo openvpn --config vpnbook-us1-tcp443.ovpn
   ```

3. **Capture traffic with Wireshark** on both:
   - Without VPN: see cleartext DNS, IPs
   - With VPN: see encrypted tunnel (e.g., port 1194 or 443 UDP)

4. **Observe Differences**:
   - Identify protocol before/after.
   - Discuss benefits of encryption.

---

### 🚨 **Lab 3: IDS/IPS with Snort or Suricata**

#### ✅ Objective:
Use Snort or Suricata to detect port scans or brute-force attacks.

#### 🛠 Tools:
- Snort or Suricata installed
- Kali Linux for attack tools (e.g., `nmap`, `hydra`)
- Wireshark (for packet validation)

---

### 🔄 Steps:
1. **Install Suricata**:
   ```bash
   sudo apt install suricata
   ```

2. **Run Suricata in live mode**:
   ```bash
   sudo suricata -i eth0 -v
   ```

3. **Simulate an attack from another VM**:
   ```bash
   nmap -sS <target IP>
   ```

4. **View Alerts**:
   - Log file: `/var/log/suricata/fast.log`
   - Look for: “TCP Port Scan” or brute force alerts.

5. **Optional**: Enable IPS mode by setting `drop` rules in `suricata.yaml`

---

## 📝 Student Deliverables:

Each lab should include:

| Task                  | What to Submit                           |
|-----------------------|------------------------------------------|
| Firewall Lab          | Screenshot of blocked ping, allowed curl |
| VPN Lab               | Wireshark capture comparing traffic      |
| IDS/IPS Lab           | Suricata log screenshot with alerts      |
| Summary               | 3-4 sentences explaining findings        |

---

## 🎯 Learning Outcome:

By completing these labs, students will:
- Understand how real-world security tools work
- Know how to build layered defenses
- Feel confident identifying and blocking malicious behavior
