### How ARP Protocol Works

**ARP (Address Resolution Protocol)** is used to map an **IP address (Layer 3)** to a **MAC address (Layer 2)** within a **local network** (e.g., Ethernet). It's essential for communication between devices on the same subnet.

#### Basic Steps:

1. **Host A** wants to send data to **Host B**, but only knows Host B's **IP address**.
2. Host A checks its ARP cache for the corresponding **MAC address**.
3. If not found, it sends an **ARP request**:

   > *"Who has IP 192.168.1.5? Tell 192.168.1.10"*
4. The target (Host B) responds with an **ARP reply**:

   > *"192.168.1.5 is at AA\:BB\:CC\:DD\:EE\:FF"*
5. Host A updates its ARP cache and sends the packet to that MAC address.



### What is ARP Poisoning (ARP Spoofing)

**ARP Poisoning** is a **man-in-the-middle (MitM) attack** where an attacker sends **fake ARP replies** to associate their own MAC address with the IP address of another device (e.g., the gateway or victim).

#### Example:

1. Attacker sends forged ARP reply to **Victim**:

   > *"192.168.1.1 (gateway) is at 11:22:33:44:55:66 (attacker's MAC)"*
2. Now, Victim thinks the attacker is the gateway.
3. Attacker also poisons the gateway with:

   > *"192.168.1.100 (victim) is at 11:22:33:44:55:66"*
4. Both gateway and victim send packets through the attacker.
5. Attacker can:

   * Intercept traffic (MitM)
   * Modify or drop packets
   * Capture credentials or sensitive data


### How to Detect/Prevent ARP Poisoning

* Use **static ARP entries** for critical devices (rarely practical at scale).
* Employ **ARP inspection tools** or **IDS/IPS systems** (e.g., `arpwatch`, `XArp`, `Snort`).
* Enable **Dynamic ARP Inspection (DAI)** on managed switches.
* Use **VPNs** to encrypt local traffic.
