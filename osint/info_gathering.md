### **Basic Network Discovery Commands**

| Command                 | Purpose                                   | Example                 |
| ----------------------- | ----------------------------------------- | ----------------------- |
| `ip a` / `ifconfig`     | Show network interfaces & IP addresses    | `ip a`                  |
| `ip route` / `route -n` | Show routing table and gateway info       | `ip route`              |
| `ping`                  | Check host availability and basic latency | `ping 8.8.8.8`          |
| `traceroute`            | Trace the route to a host                 | `traceroute google.com` |
| `whois`                 | Domain registration info                  | `whois example.com`     |
| `nslookup` / `dig`      | DNS info: A, MX, NS, TXT records          | `dig example.com ANY`   |
| `netstat -tuln`         | View open ports and listening services    | `netstat -tuln`         |
| `ss -tuln`              | Modern alternative to netstat             | `ss -tuln`              |
| `arp -a`                | View local ARP table (IP-to-MAC mapping)  | `arp -a`                |



### **Advanced Recon & Enumeration**

| Command         | Purpose                                 | Example                                 |
| --------------- | --------------------------------------- | --------------------------------------- |
| `nmap`          | Scan IPs, ports, services, OS detection | `nmap -sV -O 192.168.1.1`               |
| `netdiscover`   | Discover devices in the LAN via ARP     | `netdiscover -r 192.168.1.0/24`         |
| `tcpdump`       | Capture and analyze packets             | `tcpdump -i eth0 port 80`               |
| `wireshark`     | GUI packet sniffer (powerful analysis)  | (launch GUI)                            |
| `nc` / `netcat` | Port scanner, listener, file transfer   | `nc -v -n -z 192.168.1.1 1-1000`        |
| `enum4linux`    | Enumerate Windows shares & users        | `enum4linux 192.168.1.5`                |
| `smbclient`     | Access SMB shares                       | `smbclient //192.168.1.5/share`         |
| `nbtscan`       | NetBIOS info from Windows systems       | `nbtscan 192.168.1.0/24`                |
| `theHarvester`  | OSINT tool for emails, domains          | `theHarvester -d example.com -b google` |
| `dnsrecon`      | Advanced DNS enumeration                | `dnsrecon -d example.com`               |



### **Useful Web Recon Tools**

| Command             | Purpose                               | Example                                                                      |
| ------------------- | ------------------------------------- | ---------------------------------------------------------------------------- |
| `whatweb`           | Detect technologies used on a website | `whatweb example.com`                                                        |
| `wafw00f`           | Detect if a WAF is present            | `wafw00f example.com`                                                        |
| `nikto`             | Web server vulnerability scanner      | `nikto -h http://example.com`                                                |
| `dirb` / `gobuster` | Directory brute-forcing               | `gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt` |



###  **OSINT Commands & Tools**

| Tool                  | Function                                          |
| --------------------- | ------------------------------------------------- |
| `shodan` (CLI or Web) | Search exposed devices online                     |
| `maltego`             | Visual recon and relationship mapping             |
| `recon-ng`            | Modular OSINT framework (CLI)                     |
| `Google Dorking`      | Manual query crafting for indexed vulnerabilities |
