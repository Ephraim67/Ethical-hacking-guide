## **Module 6: Offensive Security & Ethical Hacking**

**Objectives**:
- Understand the ethical and legal boundaries of offensive security  
- Learn and apply the penetration testing lifecycle  
- Use industry-standard tools to identify, exploit, and report vulnerabilities  
- Develop responsible reporting skills and post-exploitation awareness

---

### **Topics Covered**

#### 1. **Introduction to Offensive Security**
- Offensive vs. Defensive security roles
- The role of penetration testing in cybersecurity
- Overview of common hacking methodologies (e.g., PTES, MITRE ATT&CK)

#### 2. **Reconnaissance (Passive & Active)**
- Footprinting and OSINT (e.g., Google Dorking, Shodan)
- WHOIS, DNS enumeration, Netcraft, theHarvester
- Social engineering considerations

#### 3. **Scanning & Enumeration**
- Host discovery: Ping sweep, ARP scan
- Port scanning: Nmap techniques (SYN, ACK, version detection)
- Enumeration: NetBIOS, SMB, SNMP, LDAP, RPC

#### 4. **Exploitation Techniques**
- Vulnerability exploitation concepts
- Basics of buffer overflows (stack overflow demo)
- Using Metasploit for exploiting known vulnerabilities
- Exploiting web apps: SQLi, XSS, CSRF with Burp Suite

#### 5. **Post-Exploitation & Pivoting**
- Gaining persistence
- Privilege escalation (Windows/Linux)
- Extracting credentials, lateral movement
- Covering tracks/log manipulation basics

#### 6. **Reporting & Ethical Considerations**
- Writing structured pentest reports
- Rules of engagement & scope
- Legal frameworks (Computer Fraud and Abuse Act, GDPR)
- Ethics of hacking and responsible disclosure

### **Hands-On Labs**

#### **Lab 1: Recon & OSINT**
- Use tools like `theHarvester`, `Recon-ng`, `Shodan`
- Map out an organization using publicly available data

#### **Lab 2: Scanning & Enumeration**
- Perform full host and service discovery using `Nmap` and `Enum4linux`
- Enumerate SMB shares, open ports, and OS details

#### **Lab 3: Exploitation with Metasploit**
- Use `msfconsole` to exploit known CVEs (e.g., EternalBlue on Metasploitable)
- Establish a reverse shell and demonstrate post-exploitation commands

#### **Lab 4: Web Application Hacking**
- Set up and attack DVWA/Mutillidae on local VM
- Perform XSS, SQL Injection, Command Injection using `Burp Suite`

#### **Lab 5: Buffer Overflow Demo (Advanced)**
- Walkthrough of a basic buffer overflow on a vulnerable Windows app
- Tools: Immunity Debugger, pattern_offset, mona.py

### **Deliverables**
- **Lab reports** for each exercise (screenshots, explanations)
- **Mini project**: Full attack chain on a vulnerable system (e.g., scan, exploit, escalate, report)
- **Pentest report** submission using a provided template

### **Tools Used**
- Kali Linux (main OS)
- Nmap, Metasploit, Enum4linux
- Burp Suite (Community or Pro)
- DVWA / Metasploitable / TryHackMe / HackTheBox (optional enrichment)
