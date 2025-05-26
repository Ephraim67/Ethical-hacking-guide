##  **Lecture Overview**

This lecture introduces students to **industry-standard hardening techniques** for securing operating systems, specifically Linux and Windows. It outlines common vulnerabilities, attack surfaces, and how to mitigate risks by applying configuration changes and security policies.

---

## 🎯 **Learning Objectives**

By the end of this lecture, students should be able to:

* Understand the **threat landscape** affecting OS-level security.
* Identify **key security principles** in system configuration.
* Apply practical **hardening techniques** to Linux and Windows systems.
* Use built-in tools to enforce **firewall rules, password policies**, and **logging/auditing**.

---

## 🧠 **1. Why OS Hardening Matters**

> *“A system is only as secure as its weakest configuration.”*

### Common Threats:

* **Malware** exploiting default services
* **Unauthorized access** due to weak passwords
* **Privilege escalation** through misconfigured permissions
* **Persistence mechanisms** using startup services
* **Data exfiltration** via unmonitored ports or logs

### Real-world Examples:

* EternalBlue exploiting unpatched SMB
* SSH brute force attacks on Linux servers

---

## 🔐 **2. Core Principles of OS Hardening**

| Principle                 | Explanation                                                     |
| ------------------------- | --------------------------------------------------------------- |
| **Least Privilege**       | Only give users the minimum access required.                    |
| **Reduce Attack Surface** | Disable all non-essential services and ports.                   |
| **Defense in Depth**      | Use multiple layers like firewall + auditing + password policy. |
| **Secure Defaults**       | Configure default settings to be secure from the start.         |

---

## 🐧 **3. Hardening Linux Systems**

### 🔸 Disable Unused Services

```bash
sudo systemctl list-unit-files --type=service
sudo systemctl disable bluetooth.service
```

### 🔸 Configure Firewall (UFW)

```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw allow 22/tcp
```

### 🔸 Enforce Password Policy

* File: `/etc/login.defs`, `/etc/security/pwquality.conf`
* Enforce password aging:

```bash
chage -M 90 username
```

### 🔸 Enable Auditing (`auditd`)

```bash
sudo apt install auditd
sudo auditctl -w /etc/passwd -p wa
```

### 🔸 Disable Root Login (Optional)

Edit `/etc/ssh/sshd_config`:

```bash
PermitRootLogin no
```

---

## 🪟 **4. Hardening Windows Systems**

### 🔸 Disable Unused Services

* Use `services.msc` or `sc query`
* Disable: Bluetooth, Remote Registry, Telnet

### 🔸 Windows Defender Firewall

```powershell
netsh advfirewall set allprofiles state on
```

### 🔸 Enforce Password Policy

* Open `secpol.msc` > Account Policies > Password Policy

  * Minimum length: 12+
  * Maximum age: 60 days
  * Enforce history: 5

### 🔸 Enable Auditing

* `secpol.msc` > Local Policies > Audit Policy

  * Audit logon events
  * Audit object access
  * Audit policy change

---

## 🛠️ **5. Tools for Hardening & Verification**

| Tool                     | System  | Purpose               |
| ------------------------ | ------- | --------------------- |
| `ufw`, `iptables`        | Linux   | Host firewall         |
| `auditd`                 | Linux   | Activity auditing     |
| `secpol.msc`             | Windows | Policies              |
| `netstat`, `lsof`        | Both    | Open ports monitoring |
| `chkrootkit`, `rkhunter` | Linux   | Rootkit detection     |

---

## 📊 **6. Sample Hardening Checklist**

| Task                                    | Linux         | Windows             |
| --------------------------------------- | ------------- | ------------------- |
| Disable Bluetooth                       | ✔️            | ✔️                  |
| Enable Firewall                         | ✔️ (UFW)      | ✔️ (Defender)       |
| Enforce strong password policy          | ✔️            | ✔️                  |
| Enable logging/auditing                 | ✔️ (`auditd`) | ✔️ (Event Viewer)   |
| Disable root/administrator remote login | ✔️ (SSH)      | ✔️ (Remote Desktop) |

---

## 🚧 **7. Common Mistakes to Avoid**

* Leaving SSH open to the world without key authentication
* Using weak or reused passwords
* Ignoring logs and audit trails
* Postponing OS and package updates
* Running unnecessary GUI/desktop environments on servers

---

## 📚 **8. Summary**

* Harden OS immediately after installation.
* Follow CIS benchmarks and vendor hardening guides.
* Regularly audit, patch, and verify configurations.
* Use automation tools like **Ansible**, **PowerShell DSC**, or **Bash scripts** to enforce consistency.

---

## ✅ **Next Steps / Lab**

* Students will secure Linux and Windows VMs using a provided hardening checklist.
* Submit before/after snapshots and a summary of key changes.

---

## 🧾 References

* [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks/)
* [Linux Security Hardening Guide (Red Hat)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/)
* [Microsoft Security Compliance Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=55319)

---

Would you like this lecture exported as:

* 📄 PDF?
* 🎞️ PowerPoint (PPTX)?
* 📑 Google Slides?

Let me know and I’ll generate it for you.
