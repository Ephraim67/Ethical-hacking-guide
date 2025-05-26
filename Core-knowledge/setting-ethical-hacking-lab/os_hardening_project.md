## **Project Title:**

**"Auto-Harden: Bash Script for Linux OS Hardening"**


## **Project Objectives**

* Automate common OS hardening practices using Bash.
* Learn secure configuration of services, password policies, and auditing.
* Create a reusable tool for securing Ubuntu-based systems.


##  **Project Structure**

```
auto-harden/
├── harden.sh              # Main hardening script
├── checklist.txt          # Checklist of actions performed
├── README.md              # Project documentation
└── logs/                  # Logs of script actions
```


## 🧰 **Script Features**

| Feature                            | Description                           |
| ---------------------------------- | ------------------------------------- |
| Disable unnecessary services       | Disables Bluetooth, Avahi, cups, etc. |
| Configure UFW firewall             | Blocks all except SSH and HTTP(S)     |
| Enforce password policies          | min length, expiration, complexity    |
| Lock root login over SSH           | Disables direct root access           |
| Enable audit logging               | Installs and configures `auditd`      |
| Remove guest login (optional)      | For GUI systems                       |
| Set permissions on sensitive files | e.g., `/etc/shadow`, `/etc/passwd`    |

