##  Project Title:

**MITM Attack & Network Defense Simulation with pfSense, Kali, and Windows**



###  Objectives:

* Understand and simulate ARP spoofing attacks.
* Use Wireshark to analyze traffic during an attack.
* Use pfSense firewall to detect and block malicious traffic.
* Learn to use tools like Bettercap and arpspoof for offensive operations.
* Apply network security best practices to defend endpoints.



###  Lab Architecture:

* **pfSense VM** (Firewall/DHCP/Gateway)
* **Kali Linux VM** (Attacker box – Bettercap, arpspoof, Wireshark)
* **Windows VM** (Victim workstation – browse websites, download files, etc.)

All connected to the same **virtual LAN** in something like **VirtualBox**, **VMware**, or **Proxmox**.



### Tools/Technologies:

* **Kali Linux**: Bettercap, arpspoof, Wireshark
* **pfSense**: IDS/IPS rules, DHCP, firewall logging
* **Windows**: Basic web browsing and downloading files



###  Lab Tasks / Workflow:

####  Setup Phase:

1. **pfSense Configuration:**

   * Set up as LAN gateway (192.168.1.1)
   * Enable DHCP for Windows and Kali
   * Setup firewall logging
   * Optional: Install Snort or Suricata for IDS/IPS

2. **Kali Linux Setup:**

   * Install Bettercap and Wireshark
   * Verify packet forwarding and iptables settings

3. **Windows Client:**

   * Configure DHCP or static IP in 192.168.1.x
   * Install Firefox or Chrome for browsing test



#### 🚨 Attack Simulation:

1. **Wireshark Baseline:**

   * Capture normal browsing traffic between Windows and the Internet (no attack).

2. **ARP Spoofing:**

   * Use `arpspoof` or `bettercap` from Kali to spoof Windows and pfSense
   * Intercept traffic from Windows to pfSense (default gateway)
   * Observe ARP tables and poisoning effects

3. **HTTPS Downgrade or Credential Capture:**

   * Try Bettercap modules to sniff HTTP/FTP credentials
   * Attempt DNS spoofing or redirect attempts

---

#### 🛡️ Defense Tasks:

1. **Enable Static ARP Entries on Windows** to defend against spoofing
2. **Use pfSense to detect the attacker:**

   * View ARP table anomalies
   * Enable **Snort/Suricata** and create rules for ARP/DNS poisoning
   * Block attacker’s IP/MAC
3. **Create Firewall Rules** in pfSense to block outbound spoofed packets



###  Deliverables:

* **Network topology diagram** with IP/MAC address annotations.
* **Wireshark captures** showing:

  * Normal traffic
  * ARP spoofing in progress
  * Credential capture attempts
* **Screenshots** of:

  * Bettercap/arpspoof in use
  * pfSense firewall rules and alerts
  * Windows ARP table before and after attack
* **Written report** with:

  * Attack methodology
  * Defense strategy
  * Recommendations

