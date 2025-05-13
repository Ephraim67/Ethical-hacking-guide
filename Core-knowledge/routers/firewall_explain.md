##  In-Depth Explanation: **Firewall in Computer Networks**

### **What Is a Firewall?**

A **firewall** is a **security device**—either **hardware, software**, or **both**—that controls incoming and outgoing network traffic based on **predefined security rules**. Its primary purpose is to **establish a barrier** between trusted internal networks and untrusted external networks (like the internet).



### **Firewall Goals**

1. **Prevent unauthorized access**
2. **Allow legitimate communication**
3. **Enforce company/network policies**
4. **Filter malware and threats**
5. **Log & audit access for security monitoring**



###  **How Firewalls Work: Core Concepts**

#### 1. **Packet Filtering**

* Examines packet headers: **source/destination IP, port, protocol**
* Rules determine if packets are allowed or dropped

#### 2. **Stateful Inspection**

* Keeps track of **active connections** (TCP states)
* Makes smarter decisions based on the state of a session (e.g., only allow reply packets for established connections)

#### 3. **Proxying**

* Acts as a **middleman** between client and server
* Hides internal network structure

#### 4. **Deep Packet Inspection (DPI)**

* Analyzes payload (not just headers)
* Can block application-level threats, viruses, P2P traffic, etc.


### **Firewall Rule Anatomy**

In pfSense (and most firewalls), each rule typically includes:

| Field       | Example                | Description                  |
| ----------- | ---------------------- | ---------------------------- |
| Action      | Allow / Block / Reject | What to do with the packet   |
| Interface   | LAN / WAN              | Where the rule applies       |
| Protocol    | TCP / UDP / ICMP       | Type of traffic              |
| Source      | IP/Subnet              | Where the traffic comes from |
| Destination | IP/Subnet              | Where it's going             |
| Port        | 80, 443, 22, etc.      | Target service               |
| Schedule    | Always / Time-based    | When the rule is active      |



###  **Types of Firewalls**

| Type                         | Description                        | Example                     |
| ---------------------------- | ---------------------------------- | --------------------------- |
| **Packet Filtering**         | Works on Layer 3 & 4, uses rules   | Cisco ACLs, iptables        |
| **Stateful Inspection**      | Tracks connection state            | pfSense, Cisco ASA          |
| **Application Layer**        | Blocks by app (Layer 7)            | Zscaler, Fortinet           |
| **Proxy Firewall**           | Intercepts traffic                 | Squid Proxy                 |
| **NGFW (Next-Gen Firewall)** | Combines DPI, IDS/IPS, app control | Palo Alto, pfSense+Suricata |
| **Cloud Firewalls**          | Hosted in cloud to protect VMs     | AWS Security Groups         |



###  **Firewalls in pfSense**

pfSense is a **stateful firewall**, meaning:

* It **tracks active connections** and allows return traffic automatically.
* You only need to create **outbound rules** (e.g., LAN → WAN), and return traffic is allowed.

####  In pfSense:

* Rules are **processed top-down**
* First match wins
* Default is to **deny all inbound traffic on WAN**



###  **Example Rules in pfSense**

1. **Allow LAN to Internet**

```plaintext
Interface: LAN
Action: Allow
Protocol: Any
Source: LAN net
Destination: any
```

2. **Block Social Media**

```plaintext
Interface: LAN
Action: Block
Protocol: TCP
Destination Port: 443
Destination: facebook.com (via alias or DNS)
```

3. **Allow SSH from Office IP**

```plaintext
Interface: WAN
Action: Allow
Protocol: TCP
Source: [Office IP]
Destination Port: 22
```



###  **Firewall Testing Tools**

| Tool                | Use                    |
| ------------------- | ---------------------- |
| **nmap**            | Port scanning          |
| **telnet** / **nc** | Test if ports are open |
| **Wireshark**       | See packet flows       |
| **curl** / **wget** | Test HTTP/HTTPS        |
| **hping3**          | Custom packet crafting |



###  **Advanced Firewall Features in pfSense**

* **Aliases**: Group IPs, ports, and networks
* **Schedules**: Time-based rule activation
* **Floating Rules**: Apply globally across interfaces
* **GeoIP Blocking**: Block countries or regions
* **Suricata / Snort**: IDS/IPS integration
* **pfBlockerNG**: Ad/malware domain blocking



##  **Firewall vs Other Security Layers**

| Layer       | Tool                       | Goal                                |
| ----------- | -------------------------- | ----------------------------------- |
| Network     | pfSense, Cisco ASA         | Control access                      |
| Application | WAF, Cloudflare            | Filter app traffic                  |
| Host        | Windows Firewall, iptables | OS-level filtering                  |
| Endpoint    | Antivirus, EDR             | Detect threats                      |
| Human       | Security Awareness         | Avoid phishing & social engineering |



##  Recommended Learning Path

1. **Master TCP/IP & Ports**
2. **Learn Packet Filtering vs Stateful Firewalls**
3. **Set Rules in pfSense (LAN → WAN, Block specific sites, etc.)**
4. **Enable and Test Suricata (IDS)**
5. **Practice with test attacks (Metasploit, nmap, curl)**
6. **Set up VLANs & Multi-WAN**

