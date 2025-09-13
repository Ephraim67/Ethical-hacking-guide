## Lab Setup

* **Kali Linux** → Attacker (with `bettercap`)
* **Windows Server (2019/2022)** → Victim machine (joined to network, e.g., ping or web traffic to pfSense)
* **pfSense** → Gateway/Firewall for the network

**Network Topology:**

```
Windows Server  <-->  pfSense (Gateway)  <-->  Internet
         \                         
          \                        
           Kali (Attacker)
```



## Tasks

### **Task 1 – Verify Normal Communication**

1. From Windows Server, ping the pfSense gateway IP.
2. From Kali, run Wireshark/tcpdump to observe **ARP requests/replies**.

   * Confirm Windows Server sees pfSense MAC as the gateway.



### **Task 2 – Perform ARP Poisoning**

1. On Kali, enable IP forwarding:

   ```bash
   echo 1 > /proc/sys/net/ipv4/ip_forward
   ```

2. Use **arpspoof**:

   ```bash
   # arpspoof -t <Windows_Server_IP> <pfSense_IP>
   # arpspoof -t <pfSense_IP> <Windows_Server_IP>
   ```

   This tells Windows Server and pfSense that Kali’s MAC is the other device.

3. Run Wireshark to capture traffic flowing between the two.

   * Observe that Windows traffic to pfSense now goes **through Kali**.



### **Task 3 – MITM Data Capture**

1. On Kali, run Wireshark or `ettercap -T -q -M arp /victim_IP/ /gateway_IP/`.
2. Browse from Windows Server (visit a site, log in somewhere).
3. Show captured credentials (if HTTP) or view traffic details.

### **Task 4 – Observe the Impact**

* On Windows, run `arp -a` and note the MAC address of the gateway.
* Compare before and after poisoning — it should show Kali’s MAC.



### **Task 5 – Mitigation with pfSense**

1. Enable pfSense features to **detect/mitigate spoofing**:

   * Install/add **Snort/Suricata IDS/IPS package**.
   * Enable **ARP Inspection / Anti-Spoofing** rules.
2. Re-run the attack — observe detection logs or blocked attempts.


## Deliverables

1. Screenshots of:

   * Normal ARP table on Windows Server.
   * ARP table during attack.
   * Wireshark capture showing intercepted packets.
   * pfSense logs (if mitigation is applied).
2. Short explanation:

   * How ARP Poisoning works.
   * Why pfSense/IDS can help mitigate it.
