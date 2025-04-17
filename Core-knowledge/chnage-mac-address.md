## What is a MAC Address?

**MAC** (Media Access Control) Address is a **unique hardware identifier** assigned to a device's **network interface card (NIC)**. It’s like a **fingerprint** for your device on a network.

### MAC Address Format:
Usually looks like this:
```
00:1A:2B:3C:4D:5E
```
Each pair of characters is a hexadecimal number.

### Key Points:
| Feature | Description |
|--------|-------------|
| **Unique** | Assigned by the manufacturer |
| **Layer** | Operates at Layer 2 (Data Link) of OSI model |
| **Permanent** | Stored in hardware (but can be spoofed!) |
| **Use** | Helps routers/switches identify devices |

## Why Change (Spoof) a MAC Address?

Changing your MAC address is called **MAC spoofing**, and it's useful for:

- Staying anonymous on public networks
- Bypassing MAC-based filters
- Testing network security
- Resetting Wi-Fi access time limits

## How to Change MAC Address in Kali Linux

You’ll need a **Wi-Fi adapter that supports monitor mode** (if wireless).

### 1. Check Current MAC Address

```bash
ip link show wlan0
```
or
```bash
ifconfig wlan0
```

You’ll see something like:
```
link/ether 00:11:22:33:44:55
```
### 2. Bring the Interface Down

```bash
sudo ip link set wlan0 down
```
### 3. Change the MAC Address

To a random MAC:
```bash
sudo macchanger -r wlan0
```

To a specific MAC:
```bash
sudo macchanger -m 00:11:22:33:44:55 wlan0
```

*If `macchanger` isn’t installed:*

```bash
sudo apt update && sudo apt install macchanger
```
### 4. Bring Interface Back Up

```bash
sudo ip link set wlan0 up
```
### Confirm Change

```bash
macchanger -s wlan0
```
or
```bash
ifconfig wlan0
```
