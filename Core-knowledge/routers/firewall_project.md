## ✅ **pfSense Home Lab Project – Full Guide**


### 🎯 **Project Goal**

Build a fully functional pfSense firewall/router in a virtual lab environment to:

* Simulate real-world firewall deployment
* Learn advanced firewall rules, NAT, DHCP, DNS, VPNs, VLANs
* Test IDS/IPS with Snort or Suricata
* Practice network segmentation and access control

---

## 📦 **Phase 1: Lab Setup & Installation**

---

### 🔹 Step 1: Software & Hardware Checklist

| Component                 | Description                                                             |
| ------------------------- | ----------------------------------------------------------------------- |
| pfSense ISO               | Download from [pfsense.org/download](https://www.pfsense.org/download/) |
| VirtualBox or VMware      | Virtualization platform                                                 |
| 8 GB RAM (min)            | Host machine resource                                                   |
| 1 Client OS (Kali/Ubuntu) | For LAN-side access and testing                                         |
| Optional: Wireshark       | To inspect and analyze traffic                                          |

---

### 🔹 Step 2: pfSense VM Setup

1. Open VirtualBox → `New VM` → Name: `pfSense`

2. Assign:

   * **1 core** (2 recommended)
   * **1 GB RAM**
   * **20 GB storage**

3. Add **2 Network Interfaces**:

   * **Adapter 1 (WAN)** → Attached to: `Bridged Adapter`
   * **Adapter 2 (LAN)** → Attached to: `Internal Network` → Name: `LAN`

4. Mount the pfSense ISO and start the VM.

5. Go through installer:

   * Accept defaults
   * Use Auto (UFS)
   * Reboot after install

6. Assign:

   * WAN: `em0` (bridged)
   * LAN: `em1` (internal)

Once booted, LAN IP = `192.168.1.1`

---

## 🖥️ **Phase 2: Client VM & Web Access**

---

### 🔹 Step 3: Create LAN Client VM

Create another VM (e.g., Ubuntu or Kali):

1. Network adapter: `Internal Network` → Same as pfSense LAN
2. Boot OS, configure NIC to DHCP
3. Confirm IP (e.g., `192.168.1.100`)
4. Open browser and access:

   ```
   https://192.168.1.1
   ```
5. Login: `admin / pfsense`

---

### 🔹 Step 4: pfSense Initial Configuration Wizard

* Change password
* Set hostname and domain
* Set DNS: `8.8.8.8`
* Configure WAN as DHCP
* LAN as static: `192.168.1.1/24`
* Enable DHCP on LAN
* Allow LAN-to-any rule (default)

---

## 🔐 **Phase 3: Implement Security & Features**

---

### 🔹 Step 5: Create Firewall Rules

**Test 1: Block HTTP Traffic**

* Navigate: **Firewall → Rules → LAN → Add**
* Action: Block
* Protocol: TCP
* Destination Port: 80
* Save & Apply

➡️ Try `curl http://example.com` from client → should fail

---

**Test 2: Block Facebook (via Alias)**

* **Firewall → Aliases → Add**

  * Name: `Facebook`
  * Type: `Host(s)`
  * IP/CIDR: `157.240.0.0/16`
* Create LAN rule:

  * Action: Block
  * Destination: Alias → Facebook
  * Description: `Block Facebook`

➡️ Test: open `facebook.com` — should be blocked

---

**Test 3: Time-Based Access**

* **Firewall → Schedules → Add**

  * Name: `WorkHours`, 09:00 to 17:00
* Create rule with:

  * Action: Pass
  * Source: LAN net
  * Schedule: WorkHours
  * Description: `Allow during work hours`

➡️ Outside the schedule = blocked

---

### 🔹 Step 6: Install Packages

Go to **System → Package Manager**

Recommended:

* **Snort** or **Suricata** → IDS/IPS
* **ntopng** → Real-time traffic monitoring
* **pfBlockerNG** → IP/domain blacklisting

---

## 🌐 **Phase 4: Advanced Networking**

---

### 🔹 Step 7: VLAN Lab Setup (Optional)

Simulate multiple departments:

* VLAN 10 = Admin (192.168.10.0/24)
* VLAN 20 = Users (192.168.20.0/24)

1. Enable VLANs on LAN interface
2. Assign interfaces
3. Create interface groups or rules
4. Apply segmentation firewall rules (e.g., Admin can access Users, but not vice versa)

---

### 🔹 Step 8: Setup OpenVPN Server

**VPN Access to the Lab:**

1. Go to **VPN → OpenVPN → Wizards**
2. Create a CA and certificate
3. Create server, assign tunnel network: `10.8.0.0/24`
4. Add firewall rules to allow VPN traffic
5. Export client config with **OpenVPN Export Utility**

Test with OpenVPN client from outside the lab.

---

### 🔹 Step 9: Enable Logging, Monitoring & Alerts

* **Status → System Logs → Firewall / DHCP**
* **Dashboard Widgets:** Traffic graph, firewall logs
* **Install `ntopng` or `Darkstat`**
* **Enable email alerts**

Use Wireshark in your LAN VM to inspect dropped packets and see rule effects.

---

## 💡 Final Phase: Backup & Maintain

---

### 🔹 Step 10: Backup & Snapshots

* Take VM snapshot before every major change
* **Diagnostics → Backup & Restore** → Export full config

---

## Use Cases You Can Simulate

| Scenario                                    | Tool                      |
| ------------------------------------------- | ------------------------- |
| IDS/IPS testing (e.g., Nmap scan detection) | Snort, Suricata           |
| Web content blocking                        | pfBlockerNG, Squid        |
| VPN tunneling                               | OpenVPN                   |
| Network segmentation                        | VLANs                     |
| Traffic shaping & QoS                       | Traffic Shaper            |
| Captive portal                              | pfSense built-in          |
| Access control by MAC/IP/Time               | Firewall rules, schedules |


## Skill Outcomes

By completing this lab, you'll master:

* Network interface configuration
* Firewall rule management
* DHCP/DNS/NAT
* VPN setup and access control
* Logging, alerting, and IDS/IPS
* Network segmentation and policy enforcement
