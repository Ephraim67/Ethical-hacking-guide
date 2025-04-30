## 🔹 **1. OSI & TCP/IP Models, Ports & Protocols**

### ✅ **Explanation:**
- **OSI Model** has 7 layers that describe network functions from physical media up to user-facing apps.
- **TCP/IP Model** is a 4-layer practical version used on the internet: Link, Internet, Transport, Application.
- **Ports and Protocols** help identify services on devices.
  - Example: Port 80 = HTTP, 443 = HTTPS, 22 = SSH
  - **TCP** is reliable (connection-oriented); **UDP** is faster but unreliable.

### 💡 **Lab Project Idea:**
- **Task**: Use **Wireshark** to capture a packet and identify which protocol and port is being used.
- **Objective**: Label each packet with its layer and purpose (e.g., TCP handshake, DNS query).
- **Tool**: Wireshark

---

## 🔹 **2. Firewalls, VPNs, Proxies, IDS/IPS**

### ✅ **Explanation:**
- **Firewalls** filter traffic (stateful/stateless/NGFW).
- **VPNs** create encrypted tunnels between devices/networks.
- **Proxies** act as intermediaries between users and services.
  - Forward proxy: hides client
  - Reverse proxy: hides server
- **IDS (Intrusion Detection System)** monitors traffic for suspicious activity.
- **IPS (Intrusion Prevention System)** blocks threats in real-time.

### 💡 **Lab Project Ideas:**
- **Firewall Config Lab**:
  - Use **pfSense** or `iptables` to allow only HTTP/HTTPS and block everything else.
- **VPN Lab**:
  - Set up **OpenVPN** and demonstrate encrypted vs unencrypted traffic.
- **IDS/IPS Lab**:
  - Use **Snort** or **Suricata** to generate alerts on port scans (`nmap`) or brute-force attempts.

---

## 🔹 **3. Network Access Control (802.1X)**

### ✅ **Explanation:**
- Ensures that only authenticated users/devices connect to the network.
- Uses **RADIUS** servers to validate credentials.
- Often combined with certificates or identity databases (LDAP, AD).

### 💡 **Lab Project Idea:**
- **Simulate 802.1X with FreeRADIUS**:
  - Connect a virtual machine to a network requiring credentials.
  - Try authenticated vs unauthenticated access.
  - Analyze RADIUS packet exchange with Wireshark.


## 🔹 **4. Network Segmentation & VLANs**

### ✅ **Explanation:**
- **Segmentation** limits attack surface by isolating systems.
- **VLANs** allow logical separation of networks over the same physical infrastructure.
- Helps enforce least-privilege access and limit lateral movement.

### 💡 **Lab Project Ideas:**
- **VLAN Configuration**:
  - Use a virtual switch or GNS3 to set up VLANs for "Admin," "HR," and "Guest."
  - Test communication between VLANs with ping or HTTP servers.
- **Segmentation Exercise**:
  - Use firewall rules to restrict traffic between segments.

---

## 🔬 **Lab Integration Project (Final Week)**

**Title**: “Secure Office Network Simulation”

### 🛠️ **Project Tasks**:
1. Design a network with:
   - 3 VLANs (Admin, Sales, Guests)
   - Firewall rules to isolate guest traffic
   - IDS monitoring traffic on the Sales segment
2. Simulate:
   - Unauthorized access attempts
   - Port scan
   - Misconfigured open service
3. Use:
   - Wireshark for analysis
   - Snort/Suricata for alert generation
   - OpenVPN for secure remote access
