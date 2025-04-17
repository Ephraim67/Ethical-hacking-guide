## Introduction to Network Hacking / Penetration Testing

### What Is Network Hacking?
Network hacking involves identifying and exploiting vulnerabilities in computer networks. It can be malicious (black hat), ethical (white hat), or for research (grey hat). Ethical hacking is **legal**, done with permission to **improve security**.

### What Is Penetration Testing?
Penetration Testing (or Pentesting) is a **legal, simulated cyberattack** on a system, network, or application to find and fix security flaws **before** attackers can exploit them.

> Think of it like hiring someone to break into your house so you can fix your weak locks.

## Types of Network Attacks

| **Attack** | **Description** |
|------------|-----------------|
| **Sniffing** | Capturing data packets over a network (e.g., Wireshark) |
| **Spoofing** | Faking identity (e.g., ARP Spoofing, IP Spoofing) |
| **MITM (Man-in-the-Middle)** | Intercepting and altering communication between two parties |
| **DoS/DDoS** | Flooding a server/network to make it unavailable |
| **Password Attacks** | Brute force, dictionary attacks, credential stuffing |
| **Port Scanning** | Finding open ports using tools like Nmap |

## Common Pentesting Tools

| **Tool** | **Purpose** |
|---------|-------------|
| **Nmap** | Port scanning and network discovery |
| **Wireshark** | Packet sniffing and traffic analysis |
| **Metasploit** | Exploitation framework for known vulnerabilities |
| **Hydra** | Password brute-forcing |
| **Burp Suite** | Web application testing (intercepts HTTP/S traffic) |
| **Nikto** | Web server scanner |
| **Aircrack-ng** | Wireless network testing |

## Pentesting Methodology
1. **Reconnaissance** – Gather info (passive & active)
2. **Scanning** – Identify open ports, services, vulnerabilities
3. **Gaining Access** – Exploit vulnerabilities (e.g., using Metasploit)
4. **Maintaining Access** – Create backdoors, privilege escalation
5. **Clearing Tracks** – (Not for ethical hackers! This is black hat behavior)
6. **Reporting** – Document findings and mitigation steps

## Pentest Lab Setup
- **Kali Linux** (Attacker Machine)
- **Metasploitable2** (Vulnerable Target)
- **VirtualBox or VMware** for virtualization
- Optional: **Windows VM**, **OWASP Juice Shop**, or **DVWA** for web pentesting
