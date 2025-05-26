# 🔹 **Session 1: OS Hardening & Secure Configuration**

## 🎯 **Objectives**

* Understand and apply industry best practices for securing Linux and Windows OS.
* Identify insecure default configurations and correct them.
* Use system-native tools to improve system resilience against attacks.

---

## 📚 **Topics to Cover**

### 1. **Disable Unnecessary Services**

* Why running fewer services reduces the attack surface.
* Use `systemctl`, `netstat`, `tasklist`, and `services.msc` to audit running services.

**Demo:**

* `sudo systemctl list-units --type=service` (Linux)
* `services.msc` or `sc query` (Windows)

---

### 2. **Configure Firewalls**

* Basic host-based firewall configuration.

**Linux:**

```bash
sudo ufw enable
sudo ufw allow ssh
sudo ufw deny 23
```

**Windows:**

* Use **Windows Defender Firewall** GUI or `netsh advfirewall` CLI.

---

### 3. **Enforce Strong Password Policies**

**Linux:**

* Edit `/etc/login.defs` and `/etc/security/pwquality.conf`
* Use `chage` to enforce password aging

**Windows:**

* Use `secpol.msc` → Account Policies → Password Policy
* Or: `net accounts /minpwlen:12 /maxpwage:30`

---

### 4. **Enable Logging/Auditing**

**Linux:**

* Install and configure `auditd`

```bash
sudo apt install auditd
sudo auditctl -w /etc/passwd -p wa
```

**Windows:**

* Enable auditing via `secpol.msc` → Local Policies → Audit Policy

---

## 🧰 **Tools Needed**

| Tool                         | System  | Purpose                           |
| ---------------------------- | ------- | --------------------------------- |
| `ufw`                        | Linux   | Firewall                          |
| `auditd`                     | Linux   | File and event auditing           |
| `Group Policy Editor`        | Windows | Password and audit policies       |
| `services.msc`, `netstat`    | Windows | Manage services and network ports |
| `systemctl`, `ps`, `netstat` | Linux   | Monitor and manage services       |

---

## 🧪 **Lab Activity: OS Hardening Checklist**

**Instructions:**
Students work in pairs or solo using:

* A Linux VM (Ubuntu/Kali)
* A Windows 10/11 VM (with admin access)

### ✅ Checklist Example

| Task                                | Linux                 | Windows               |
| ----------------------------------- | --------------------- | --------------------- |
| Disable unnecessary services        | ✔️                    | ✔️                    |
| Enable firewall                     | ✔️ (`ufw`)            | ✔️ (Windows Defender) |
| Enforce password policy             | ✔️ (`login.defs`)     | ✔️ (`secpol.msc`)     |
| Enable logging/audit logs           | ✔️ (`auditd`)         | ✔️ (Audit Policy)     |
| Verify no unused network ports open | ✔️ (`netstat -tulnp`) | ✔️ (`netstat -an`)    |

---

## 🧠 **Discussion / Debrief Questions**

* What services did you find running by default that weren’t needed?
* How did firewall rules differ between Linux and Windows?
* What are the consequences of poor logging?

---

## 📝 **Assessment / Deliverable**

* Students submit screenshots and a summary of the changes made.
* Include firewall rules, disabled services, and audit policy screenshots.
* Optionally, perform a short reflective quiz (e.g., why disable unused ports?)

