### Targeted Packet Sniffing – Zeroing In Like a Pro

Targeted packet sniffing is all about **focusing your sniffing tool on a specific device, access point (AP), or type of traffic** — instead of blindly capturing everything. This is much more efficient and stealthy in pentesting scenarios.

## Why Target?
- To capture **handshakes** from a specific Wi-Fi network
- To sniff data between **two known IPs or MAC addresses**
- To avoid noise (irrelevant packets)
- To be stealthier and faster

## Step-by-Step: Targeted Sniffing with `airodump-ng`

### Requirements:
- Wireless adapter in **monitor mode**
- Know your target's **BSSID** (MAC address of the AP)
- Know the **channel** the AP is on

### Find the Target First

```bash
sudo airodump-ng wlan0mon
```

- Note:
  - `BSSID` of the AP (e.g., `00:11:22:33:44:55`)
  - `CH` (channel, e.g., `6`)

### Target Specific AP

```bash
sudo airodump-ng wlan0mon --bssid 00:11:22:33:44:55 --channel 6 -w capture
```

This will:
- Only listen to the chosen AP (BSSID)
- Only on the selected channel (faster capture)
- Save to file (`capture.cap`)

> This is **ideal for capturing WPA handshakes** from one access point!

### Want to Target a Specific Client Too?

You can **track a specific client** connecting to the AP by using the **Station MAC** (STA) from the `airodump-ng` output.

## Targeted Sniffing with `tcpdump`

### Filter by IP Address:

```bash
sudo tcpdump -i wlan0 ether host AA:BB:CC:DD:EE:FF
```

This captures packets **to or from** that MAC address.

Or:

```bash
sudo tcpdump -i wlan0 host 192.168.1.10
```

Captures packets **to/from that IP**.

### Filter by Port:

```bash
sudo tcpdump -i wlan0 port 80
```

Captures only **HTTP traffic**.
