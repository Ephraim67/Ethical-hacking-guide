### Intercepting Network Traffic: Overview

Intercepting (or **sniffing**) network traffic means capturing data packets as they travel across the network. This can be used for legitimate purposes like **network diagnostics**, **monitoring**, and **intrusion detection**, or for **malicious activities** such as **eavesdropping**, **credential theft**, or **data manipulation**.


### Common Methods of Interception

#### 1. **Packet Sniffing**

* Tools: `Wireshark`, `tcpdump`, `Ettercap`
* Requires: Access to the same network segment (e.g., LAN, Wi-Fi)
* Works by setting the NIC into **promiscuous mode** to capture all packets.

#### 2. **ARP Poisoning + MITM**

* As explained earlier, this allows an attacker to reroute traffic through their device.
* Tools: `Ettercap`, `Bettercap`, `Cain & Abel`
* Once traffic is flowing through the attacker's machine, it can be sniffed, modified, or dropped.

#### 3. **Rogue Access Points**

* An attacker creates a **fake Wi-Fi access point** to trick users into connecting.
* Traffic is routed through the attacker's machine.
* Tools: `Airbase-ng`, `Fluxion`, `WiFi Pumpkin`

#### 4. **DNS Spoofing**

* Redirects domain requests to malicious IPs.
* Often combined with ARP poisoning.
* Tools: `dnsspoof`, `Bettercap`

#### 5. **Port Mirroring (on switches)**

* On managed switches, administrators can configure a **SPAN port** to copy traffic for monitoring.

#### 6. **SSL Stripping**

* Converts HTTPS traffic to HTTP to intercept readable data.
* Tools: `sslstrip`, `Bettercap`
* Mitigated by HSTS and browser protections.


### Countermeasures and Defenses

| Threat                 | Defense                                                  |
| ---------------------- | -------------------------------------------------------- |
| ARP Poisoning          | Dynamic ARP Inspection, Static ARP, Secure switches      |
| Sniffing on Open Wi-Fi | Use VPNs or enforce WPA3 encryption                      |
| Rogue APs              | Enable AP detection, educate users, use enterprise Wi-Fi |
| SSL Stripping          | Enforce HTTPS, use HSTS, inspect cert chains             |
| General Interception   | Network segmentation, IDS/IPS, switch hardening          |
