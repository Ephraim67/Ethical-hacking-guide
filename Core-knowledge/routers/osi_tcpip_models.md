# **Module Topic: OSI & TCP/IP Models, Ports & Protocols**


## **In-Depth Explanation**

### OSI Model (7 Layers)
| Layer | Name               | Description                                               | Example Protocols            |
|-------|--------------------|-----------------------------------------------------------|-------------------------------|
| 7     | Application         | End-user access to network (interface)                    | HTTP, FTP, DNS, SMTP          |
| 6     | Presentation        | Data formatting, encryption, compression                  | SSL, TLS, JPEG                |
| 5     | Session             | Manages connections (start/stop sessions)                 | NetBIOS, RPC                  |
| 4     | Transport           | End-to-end delivery, flow control                         | TCP, UDP                      |
| 3     | Network             | Logical addressing and routing                            | IP, ICMP                      |
| 2     | Data Link           | MAC addressing, framing, and error detection              | Ethernet, ARP, PPP            |
| 1     | Physical            | Physical transmission (cables, radio, voltages)           | Ethernet cables, Wi-Fi, etc.  |


### TCP/IP Model (4 Layers)
| Layer         | Maps To OSI | Description                             |
|---------------|-------------|-----------------------------------------|
| Application   | 7,6,5        | High-level communication services       |
| Transport     | 4           | Reliable or fast delivery (TCP/UDP)     |
| Internet      | 3           | Routing and addressing (IP)             |
| Link          | 2,1         | Local physical network transmission     |


### Ports & Protocols
- Port numbers identify services.
- **Well-known ports** (0–1023):
  - Port 80: HTTP
  - Port 443: HTTPS
  - Port 22: SSH
  - Port 53: DNS
  - Port 25: SMTP
- **TCP**:
  - Reliable, connection-based (ensures data arrives).
  - Used for HTTP, HTTPS, FTP.
- **UDP**:
  - Fast, connectionless (no guarantee).
  - Used for video streaming, DNS, VoIP.


## **Lab Project: Packet Capture with Wireshark**

### **Goal**:
You will observe how network communication happens across OSI layers and which ports and protocols are used.


## **Tools Required**:
- Wireshark (Install from https://www.wireshark.org/)
- Internet connection or LAN
- Browser and terminal/command prompt


## **Steps to Complete the Lab**:

### **1. Install and Open Wireshark**
- Launch Wireshark.
- Select your active network interface (e.g., `Wi-Fi`, `eth0`).
- Click **Start Capture**.

### **2. Generate Traffic**
You are to:
- Open a browser and visit: `http://example.com`
- Open a terminal and run:  
  - `ping google.com`
  - `nslookup google.com`
  - Optional: `curl http://example.com`



### **3. Stop the Capture**
- After ~30 seconds, stop the capture by clicking the red square icon.



### **4. Analyze Traffic**
Use filters:
- `http` – View HTTP requests/responses
- `tcp` – View all TCP traffic
- `udp` – View all UDP traffic
- `dns` – View DNS lookups


### **5. Identify Protocols & Ports**
For each selected packet:
- Right-click → **Follow TCP stream** (if applicable)
- Examine:
  - **Source IP**
  - **Destination IP**
  - **Protocol**
  - **Source Port / Destination Port**
  - **Payload (data)**


### **6. Map to OSI Layers**
- Classify what layer the packet belongs to:
  - TCP Handshake → Layer 4
  - DNS Query → Layer 7 (App) & 4 (UDP) & 3 (IP)
  - Ethernet II info → Layer 2
- Take **screenshots** and label layers


### 📝 **Deliverables**:
Each student should submit:
- Screenshots of 3 different protocols (HTTP, DNS, TCP handshake)
- A table mapping each packet to:
  - Protocol
  - Port
  - OSI Layer
  - Description

Example:

| Packet | Protocol | Port | OSI Layer(s) | Description                |
|--------|----------|------|---------------|----------------------------|
| 1      | TCP      | 443  | 4             | HTTPS connection setup     |
| 2      | DNS      | 53   | 7, 4, 3        | Resolving google.com       |
| 3      | HTTP     | 80   | 7              | GET request for a web page |



**You will be able to:**
- Understand protocol behavior
- Map traffic to the OSI model
- Recognize port usage
- Gain confidence using packet analysis tools
