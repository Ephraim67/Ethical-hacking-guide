### Step-by-Step Traffic Analysis Guide


### 1. **Identify the Scanning Host**

* **Filter to isolate the scan:**
  In Wireshark, use:

  ```plaintext
  ip.src == 192.168.x.x && ip.dst == 192.168.x.x
  ```

  or

  ```plaintext
  tcp.flags.syn == 1 && tcp.flags.ack == 0
  ```
* Look for:

  * One host sending SYN packets to many different ports on another host.
  * A high frequency of packets in a short time to different ports.

> **Challenge Q1: What is the IP responsible for conducting the port scan activity?**
> Look at `ip.src` for the SYN packets to multiple ports.

---

### 2. **Determine Port Range Scanned**

* Sort captured traffic by **Destination Port**.
* Note the **lowest and highest port numbers** scanned.

> **Challenge Q2: What is the port range scanned by the suspicious host?**
> Format: `firstport-lastport`

---

### 3. **Identify Scan Type**

* SYN packets without completing TCP handshake = **SYN scan**.
* SYN followed by RST = **Half-open scan**.
* TCP connect with 3-way handshake = **Connect scan**.
* Use `tcp.flags.syn == 1` and check if there's an ACK.

> **Challenge Q3: What is the type of port scan conducted?**
> Format: `TCP Syn` or `TCP Connect`



### 4. **Detect Additional Recon Tools**

* Look for **User-Agent**, **Payload Strings**, or **HTTP GET/POST** headers.

* Filter using:

  ```plaintext
  http.request
  ```

  or look in the **Info** column for suspicious requests.

* Tools like **Nmap**, **Nikto**, **Gobuster**, or **dirb** often include version info in requests.

> **Challenge Q4: Two more tools used to perform reconnaissance?**
> Example: `Nikto 2.1.6, Gobuster 3.1.0`



### 5. **Find the PHP Upload Point**

* Filter:

  ```plaintext
  http.request.method == "POST"
  ```

  or search for `.php` file uploads in the **Info** column or **Follow HTTP stream**.
* Look for the file where attacker uploads the web shell.

> **Challenge Q5: Name of the PHP file used to upload web shell?**
> Look for the target endpoint of the POST request.

---

### 6. **Identify Web Shell Filename**

* After upload, attacker might access the web shell:

  ```plaintext
  http.request.uri contains ".php"
  ```
* Look at accessed PHP file names.

> **Challenge Q6: Name of the uploaded web shell?**
> Example: `cmd.php`, `shell.php`, etc.

---

### 7. **Find Parameter Used for Command Execution**

* In the HTTP requests to the web shell, look at the GET or POST parameters:
  Example:

  ```
  http://victim/shell.php?cmd=whoami
  ```

> **Challenge Q7: Parameter used in web shell for executing commands?**
> e.g., `cmd`, `exec`, `command`, etc.

---

### 8. **First Command Executed**

* In the HTTP request that follows upload, check first value passed in the shell:

  ```plaintext
  whoami, uname -a, id, etc.
  ```

> **Challenge Q8: First command executed by attacker?**
> Likely something like `whoami` or `id`.

---

### 9. **Shell Connection Type**

* Look for outgoing reverse shell attempts:

  * `tcp.stream` showing `/bin/bash` or `/bin/sh`
  * Look for `bash -i >& /dev/tcp/...`
  * Shells over `netcat`, `python`, or `php`

> **Challenge Q9: Type of shell connection obtained?**
> e.g., `Reverse TCP`, `Reverse Bash`, `Reverse Netcat`

---

### 10. **Port Used for Shell Connection**

* Once you detect the shell attempt, check the **destination port** on the attacker's system:

  ```plaintext
  tcp.port == x
  ```

> **Challenge Q10: What is the port he uses for the shell connection?**
> Check TCP stream of shell connection.
