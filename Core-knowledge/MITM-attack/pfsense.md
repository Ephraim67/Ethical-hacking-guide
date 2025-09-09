## 🖥️ What You’ll End Up With

* **pfSense VM** = Your virtual router/firewall.
* **WAN (Adapter 1)** = NAT (gives pfSense internet access through your host).
* **LAN (Adapter 2)** = Internal Network (isolated network for Kali & Windows).
* **Kali Linux & Windows VMs** = Connected to the LAN network, getting DHCP from pfSense.

---

## 🔹 Step 1: Create pfSense VM in VirtualBox

1. Download the pfSense ISO from [pfsense.org](https://www.pfsense.org/download/).
2. In VirtualBox, create a **new VM**:

   * Type: **BSD**
   * Version: **FreeBSD (64-bit)**
   * RAM: **2 GB** minimum.
   * Disk: **10 GB** minimum.
3. Add the pfSense ISO as a virtual optical disk under **Storage**.

---

## 🔹 Step 2: Configure pfSense Network Adapters

In pfSense VM settings:

1. **Adapter 1 (WAN):**

   * Enable, choose **NAT**.
2. **Adapter 2 (LAN):**

   * Enable, choose **Internal Network**.
   * Name it (e.g., `pfsenseLAN`).

---

## 🔹 Step 3: Install pfSense

1. Boot the pfSense VM.
2. Go through the installation wizard (accept defaults, ZFS/Auto partition is fine).
3. After installation, pfSense will reboot.
4. At the console, pfSense will auto-detect interfaces:

   * **WAN** = Adapter 1 (NAT).
   * **LAN** = Adapter 2 (Internal Network).

---

## 🔹 Step 4: Assign LAN IP

1. In the pfSense console, choose **Option 2: Set Interface(s) IP Address**.
2. Select LAN and set:

   ```
   IP: 192.168.1.1
   Subnet: 24 (255.255.255.0)
   No upstream gateway needed.
   Enable DHCP: Yes (e.g., range 192.168.1.100 - 192.168.1.200)
   ```
3. pfSense LAN will now provide DHCP to VMs.

---

## 🔹 Step 5: Configure Kali Linux VM

1. Create/start your Kali Linux VM.
2. In Kali’s VM **Settings > Network**:

   * Adapter 1 = **Internal Network**.
   * Choose the same network name (`pfsenseLAN`).
3. Start Kali, it should get an IP like `192.168.1.101` from pfSense.

---

## 🔹 Step 6: Configure Windows VM

1. Create/start your Windows VM.
2. In Windows VM **Settings > Network**:

   * Adapter 1 = **Internal Network**.
   * Same network name (`pfsenseLAN`).
3. Start Windows, it should also get a LAN IP (e.g., `192.168.1.102`).

---

## 🔹 Step 7: Access pfSense Web GUI

1. On Kali or Windows, open a browser:

   ```
   https://192.168.1.1
   ```
2. Login:

   ```
   Username: admin
   Password: pfsense
   ```
3. Run the **Setup Wizard** to set hostname, DNS, passwords, etc.

---

## 🔹 Step 8: Test Connectivity

* From Kali/Windows, try pinging `8.8.8.8` or opening a website.
* pfSense is now routing traffic from LAN → WAN.

---

### 🔹 Summary Table of VM Network Settings

| VM             | Adapter 1                       | Adapter 2                       |
| -------------- | ------------------------------- | ------------------------------- |
| **pfSense**    | NAT (WAN)                       | Internal Network (`pfsenseLAN`) |
| **Kali Linux** | Internal Network (`pfsenseLAN`) | None                            |
| **Windows**    | Internal Network (`pfsenseLAN`) | None                            |

---

Would you also like me to include a **diagram** showing how pfSense, WAN, LAN, and your VMs connect visually?
