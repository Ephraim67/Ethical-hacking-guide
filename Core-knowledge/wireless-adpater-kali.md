Connecting a **wireless adapter** to **Kali Linux** (especially inside a VM like VirtualBox or VMware) is a key step for Wi-Fi hacking, packet sniffing, and wireless pentesting. Step-by-step guide for **USB Wi-Fi adapter setup** on Kali.

## Requirements

### What You’ll Need:
- Kali Linux (preferably updated)
- A compatible **external USB Wi-Fi adapter** that supports **monitor mode** and **packet injection**
  - Recommended chipsets: **Atheros**, **Realtek RTL8812AU**, **Ralink**, etc.
- If using **VirtualBox or VMware**, make sure:
  - USB 2.0 or 3.0 is enabled
  - Extension pack is installed (VirtualBox)
  - VMware Tools are installed (VMware)

## Step-by-Step: VirtualBox

### 1. Plug in Your Wi-Fi Adapter
Plug it into your physical USB port.

### 2. Enable USB Support
- Go to **Settings → USB** in VirtualBox
- Select **USB 2.0 or USB 3.0**
- Click the **+ icon** and select your Wi-Fi adapter from the list

### 3. Start Kali VM
Boot into Kali. The adapter should now be detected.

## Step-by-Step: VMware

### 1. Plug in the Adapter
Insert your USB adapter into your machine.

### 2. Connect USB Device
When Kali is running:
- Go to **VM → Removable Devices**
- Select your adapter → **Connect (Disconnect from Host)**

## Verifying the Adapter in Kali

### Run these commands in Terminal:

```bash
ifconfig
```
or
```bash
ip a
```

You should see something like `wlan0` or `wlan1`.

Then run:

```bash
iwconfig
```

You should see:
```plaintext
wlan0     IEEE 802.11  Mode:Managed  Access Point: Not-Associated
```
## Enabling Monitor Mode

To enable monitor mode:

```bash
sudo airmon-ng start wlan0
```

You’ll now see an interface like `wlan0mon`. Confirm with:

```bash
iwconfig
```

To stop monitor mode:

```bash
sudo airmon-ng stop wlan0mon
```
## Test Packet Injection

You can test with:

```bash
sudo aireplay-ng --test wlan0mon
```

## Troubleshooting Tips

| Problem | Solution |
|--------|----------|
| Adapter not showing up | Ensure USB is passed to VM correctly |
| Still not working | Use Kali on bare metal or use **Live USB Boot** |
| No monitor mode | Ensure your adapter supports it (many cheap adapters don't) |
| "Device busy" errors | Kill conflicting processes: `sudo airmon-ng check kill` |
