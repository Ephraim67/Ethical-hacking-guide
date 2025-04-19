## What Are Wi-Fi Bands?

Wi-Fi operates on **radio frequencies**. The two main bands are:

- **2.4 GHz** (Gigahertz)
- **5 GHz**

Each band is made up of **channels**, which devices use to communicate wirelessly

## Comparison: 2.4GHz vs. 5GHz

| Feature | 2.4 GHz | 5 GHz |
|--------|--------|--------|
| **Range** | Longer (better wall penetration) | Shorter |
| **Speed** | Slower | Faster |
| **Interference** | High (used by microwaves, Bluetooth, etc.) | Low |
| **Channels** | 14 (but overlap) | 23+ (non-overlapping) |
| **Best Use** | Farther distances, obstacles | High-speed, short range |

### Channels Overview

#### 2.4 GHz Channels:
- Channels **1 to 14** (only 1, 6, and 11 are non-overlapping)
- Used by most IoT devices

#### 5 GHz Channels:
- Channels **36 to 165**
- More **non-overlapping** channels = less interference
- Supports **higher data rates** (AC/AX standards)

## How to Check Band Support in Kali

### Check Available Bands for Adapter

```bash
sudo iw list
```

Look under:
```
Frequencies:
  * 2412 MHz [1] (20.0 dBm)
  * 5180 MHz [36] (20.0 dBm)
```

That tells you which **bands and channels** your adapter supports.

## Real-World Use in Pentesting

| Scenario | Recommended Band |
|----------|------------------|
| Wardriving (long range) | 2.4GHz |
| Cracking faster Wi-Fi (less noise) | 5GHz |
| Capturing handshake from AP far away | 2.4GHz |
| Testing modern routers (WPA3, 802.11ac) | 5GHz |

## Bonus: Set Wi-Fi Band in Monitor Mode

You can force your adapter to scan a specific band using `airodump-ng`:

```bash
sudo airodump-ng wlan0mon --band a
```

- `--band b/g` → 2.4GHz  
- `--band a` → 5GHz


## Prerequisites
- You **must have a Wi-Fi adapter** that supports **monitor mode** and **5GHz**.
- Put the adapter into **monitor mode** first.

```bash
sudo airmon-ng start wlan0
```

You’ll get something like `wlan0mon`.
## Command to Capture 5GHz Traffic

```bash
sudo airodump-ng wlan0mon --band a
```

- `--band a` → **5GHz only**
- This scans **channels like 36, 40, 44, 48, etc.**

## Command to Capture 2.4GHz Traffic

```bash
sudo airodump-ng wlan0mon --band bg
```

- `--band b` = 802.11b (2.4GHz)
- `--band g` = 802.11g (2.4GHz)
- Often just `--band bg` is enough for most 2.4GHz APs

## Capture Both 2.4GHz and 5GHz Together

```bash
sudo airodump-ng wlan0mon --band abg
```

- `--band abg` → scan **all available channels in both bands**

Note: Scanning both bands can be slower, since `airodump` hops between many more channels.

## To Save Captured Data (Packets)

```bash
sudo airodump-ng wlan0mon --band abg -w capture
```

- `-w capture` → writes output files:
  - `capture.cap` (packet capture)
  - `capture.csv` (AP/client info)
  - `capture.kismet.csv`

## Optional: Focus on Specific Channel

To stay fixed on a single channel (faster handshake capture):

```bash
sudo airodump-ng wlan0mon --channel 36 -w capture
```
## Pro Tip: Combine with Wireshark

If you want to live-capture and analyze traffic:

```bash
sudo wireshark &
```

Then select `wlan0mon` and apply filters like:

- `wlan.fc.type_subtype == 0x08` (Beacon frames)
- `eapol` (for WPA/WPA2 handshakes)
