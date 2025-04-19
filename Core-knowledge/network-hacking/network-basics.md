## **Network Basics: The Foundation of Communication**

### What is a Network?
A **network** is a group of two or more computers or devices that are connected to share data and resources (like files, printers, internet)

## Types of Networks

| Type | Description |
|------|-------------|
| **LAN (Local Area Network)** | Small area network like a home, office, or building. |
| **WAN (Wide Area Network)** | Covers large areas; the internet is the biggest WAN. |
| **MAN (Metropolitan Area Network)** | Spans a city or campus. |
| **PAN (Personal Area Network)** | Very small, like Bluetooth between a phone and speaker. |


## Common Network Devices

| Device | Function |
|--------|----------|
| **Router** | Connects different networks together (e.g., LAN to internet). |
| **Switch** | Connects devices within a LAN; more efficient than a hub. |
| **Hub** | Broadcasts data to all devices; outdated. |
| **Access Point** | Extends Wi-Fi to wireless devices. |
| **Firewall** | Controls incoming/outgoing traffic based on rules. |

### IP Address:
A unique identifier for a device on a network.

- **IPv4:** `192.168.1.1` (most common)
- **IPv6:** `2001:0db8:85a3::8a2e:0370:7334` (newer, more addresses)

### Types of IP:

| Type | Example | Use |
|------|---------|-----|
| **Public IP** | 8.8.8.8 | Visible on the internet |
| **Private IP** | 192.168.x.x | Used within LAN |
| **Loopback** | 127.0.0.1 | Refers to “yourself” |

## TCP/IP Model (4 Layers)

| Layer | Description |
|-------|-------------|
| **Application** | Interfaces with apps (HTTP, FTP, DNS) |
| **Transport** | Ensures reliable delivery (TCP/UDP) |
| **Internet** | Handles addressing & routing (IP) |
| **Network Access** | Deals with hardware (Ethernet, Wi-Fi) |

## TCP vs UDP

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Yes | No |
| Speed | Slower | Faster |
| Reliability | Reliable (ACKs) | Unreliable |
| Use Case | Web, Email | Streaming, DNS, VoIP |

## Common Network Protocols

| Protocol | Port | Description |
|----------|------|-------------|
| **HTTP** | 80 | Web traffic (insecure) |
| **HTTPS** | 443 | Secure web traffic |
| **FTP** | 21 | File transfer |
| **SSH** | 22 | Secure remote login |
| **DNS** | 53 | Domain name resolution |
| **SMTP** | 25 | Email sending |
| **DHCP** | 67/68 | Auto IP assignment |

## Extra Terms to Know

- **MAC Address:** Hardware address, unique to each NIC (e.g., `00:0A:E6:3E:FD:E1`)
- **DNS (Domain Name System):** Translates domains (`google.com`) into IP addresses
- **Subnet:** Logical segmentation of a network
- **NAT (Network Address Translation):** Maps private IPs to a public IP
