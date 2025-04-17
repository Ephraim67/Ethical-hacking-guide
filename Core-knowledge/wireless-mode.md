## Wireless Modes: Explained

Your wireless adapter can work in **different modes**, depending on what you're trying to do.

### 1. **Managed Mode** (a.k.a. "Client Mode")

- **Default mode** for most devices  
- Used when **connecting to Wi-Fi routers**
- Your adapter **associates with an Access Point (AP)**
- You can **browse the internet**, stream, etc.

Example:
```bash
iwconfig wlan0
```
Output might show:
```
Mode:Managed
```

### 2. **Monitor Mode**

**Special mode for sniffing packets**  
- Your adapter **does NOT associate** with any AP
- It listens to **all traffic** in the air — even if it's not meant for your device
- Required for tools like **aircrack-ng, airodump-ng, Wireshark (wireless sniffing)**

Example:
```bash
iwconfig wlan0mon
```
Output might show:
```
Mode:Monitor
```
## How to Set Wireless Modes in Kali Linux

### Step-by-Step:

#### 1. Identify Your Interface

```bash
iwconfig
```
Look for something like `wlan0`.

#### 2. Put the Interface Down

```bash
sudo ip link set wlan0 down
```

#### 3. Switch to Monitor Mode

```bash
sudo iwconfig wlan0 mode monitor
```

or use:
```bash
sudo airmon-ng start wlan0
```

➡ This creates `wlan0mon` or similar interface.

#### 4. Bring It Back Up

```bash
sudo ip link set wlan0 up
```

#### 5. Confirm Mode

```bash
iwconfig
```

You should now see:
```
Mode:Monitor
```
### To Revert Back to Managed Mode:

```bash
sudo airmon-ng stop wlan0mon
```
OR
```bash
sudo ip link set wlan0 down
sudo iwconfig wlan0 mode managed
sudo ip link set wlan0 up
```
## Pro Tip: Kill Conflicting Services

Sometimes NetworkManager or wpa_supplicant can interfere. Run:

```bash
sudo airmon-ng check kill
```

(You can restart services later with `sudo service NetworkManager restart`)
