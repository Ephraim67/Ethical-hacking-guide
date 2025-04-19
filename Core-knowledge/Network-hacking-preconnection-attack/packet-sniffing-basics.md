## What is Packet Sniffing?

**Packet sniffing** is the process of **capturing, intercepting, and analyzing network traffic (packets)** as they travel across a network.

Think of it as:
> "Wiretapping the network to see what devices are saying to each other."


## Why Learn Packet Sniffing?

| Use Case | Purpose |
|----------|---------|
| **Troubleshooting** | Diagnose slow or failing network connections |
| **Security Analysis** | Detect suspicious or malicious traffic |
| **Password Sniffing** | Capture plaintext credentials (e.g., FTP, HTTP) during pentesting |
| **Reconnaissance** | Identify live hosts, devices, and protocols |
| **Training & Education** | Learn how protocols work under the hood |

## How Does Packet Sniffing Work?

When data is sent over a network, it's broken into small **packets**. Each packet includes:
- Source IP & MAC
- Destination IP & MAC
- Protocol info (TCP, UDP, HTTP, etc.)
- Payload (actual content)

A **sniffer** captures these packets from the network interface.

## Popular Packet Sniffing Tools

| Tool | Use |
|------|-----|
| **Wireshark** | GUI-based, great for deep inspection |
| **tcpdump** | Terminal-based, lightweight |
| **tshark** | CLI version of Wireshark |
| **airodump-ng** | Wi-Fi sniffing (for monitor mode) |
| **Ettercap** | ARP spoofing + packet sniffing |

## How to Sniff Packets (Kali Linux Example)

### Using `tcpdump`:

```bash
sudo tcpdump -i wlan0
```

Filter by port:

```bash
sudo tcpdump -i wlan0 port 80
```

Save to a file:

```bash
sudo tcpdump -i wlan0 -w capture.pcap
```

### Using `Wireshark`:

```bash
sudo wireshark
```

1. Select your network interface (like wlan0 or wlan0mon)
2. Hit **Start**
3. Use filters like:
   - `http`
   - `ip.addr == 192.168.1.1`
   - `tcp.port == 443`

Wireshark captures everything in real-time — perfect for analysis.

### Using `airodump-ng` (for Wi-Fi sniffing):

```bash
sudo airmon-ng start wlan0
sudo airodump-ng wlan0mon
```

This shows nearby Wi-Fi networks and connected devices — useful for wireless hacking.

```bash
iwconfig mon0
```

```bash
airodump-ng mon0
```
