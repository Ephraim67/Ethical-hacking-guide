### **Project Overview: pfSense Home Lab Setup**

**Goal:** Build a network security lab using pfSense to practice routing, firewall rules, VPNs, VLANs, and IDS/IPS.



### **Step-by-Step Guide**

### **Step 1: Understand the Architecture**

Decide on your setup:

* **Virtualized Lab:** pfSense installed in a hypervisor (e.g., VirtualBox, VMware, Proxmox).
* **Bare Metal:** pfSense installed on dedicated hardware/router.

 **Common Virtual Setup**:

* 1 WAN interface (bridged to your host’s network)
* 1 LAN interface (internal network for virtual machines)



### **Step 2: Download pfSense**

* Go to [https://www.pfsense.org/download/](https://www.pfsense.org/download/)
* Choose:

  * **Architecture:** AMD64 (most common)
  * **Installer type:** ISO Installer (for virtualization or USB boot)
  * **Mirror:** Any close to you



### **Step 3: Create Virtual Machines**

In **VirtualBox**, **VMware**, or **Proxmox**:

* Create a VM with:

  * 2 vNICs (1 bridged for WAN, 1 internal for LAN)
  * 1 GB RAM, 20 GB HDD
  * Mount pfSense ISO

**Enable Intel VT-x/AMD-V** in BIOS for virtualization.



### **Step 4: Install pfSense**

1. Boot from the ISO
2. Choose default settings (install to disk, use UFS)
3. Reboot after installation
4. Set up interfaces:

   * WAN: bridged adapter (internet access)
   * LAN: internal network (lab)



### **Step 5: Access pfSense Web GUI**

1. Boot up pfSense and find the LAN IP (e.g., `192.168.1.1`)
2. Create another VM (e.g., Kali, Ubuntu) connected to the LAN network
3. Open browser → go to `https://192.168.1.1`
4. Default login: `admin / pfsense`



### **Step 6: Basic Configuration**

* Change admin password
* Set hostname, DNS, and NTP servers
* Configure DHCP for LAN
* Enable SSH access (optional)



### **Step 7: Add Lab Machines**

Create additional VMs (e.g., Windows, Linux) connected to the LAN network.

* Use these for testing firewall rules, VLANs, VPNs, IDS/IPS.



### **Step 8: Setup Scenarios**

Here are some fun and educational scenarios to implement:

| Scenario            | Description                                   |
| ------------------- | --------------------------------------------- |
| **Firewall Rules**  | Allow/block traffic by port, IP, and protocol |
| **VLANs**           | Segment the network into departments          |
| **OpenVPN Server**  | Access your lab remotely and securely         |
| **Squid Proxy**     | Monitor and control internet usage            |
| **Snort/Suricata**  | Intrusion detection and prevention            |
| **Captive Portal**  | Set up a guest Wi-Fi with login page          |
| **Traffic Shaping** | Manage bandwidth and prioritize traffic       |



### **Step 9: Logging and Monitoring**

* Enable **Syslog** for logs
* Set up **Dashboard widgets**
* Use **pfTop** and **ntopng** for traffic visibility



### **Step 10: Backup & Snapshots**

* Export pfSense config (Diagnostics → Backup & Restore)
* Take VM snapshots before major changes



## Tools You’ll Use

* **pfSense**
* **VirtualBox / VMware / Proxmox**
* **Kali Linux** or **Windows** VMs
* **Wireshark** (for traffic capture)
* **nmap**, **curl**, **netcat** (for testing)
