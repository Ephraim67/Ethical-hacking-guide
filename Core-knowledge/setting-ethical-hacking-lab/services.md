# 🐧 **Linux: List All Services**

### 🔹 Using `systemctl` (modern systems with `systemd`)

```bash
systemctl list-unit-files --type=service
```

* Shows **all services** with their **status**: `enabled`, `disabled`, `static`, etc.

To see which services are **actively running**:

```bash
systemctl list-units --type=service --state=running
```

To check the **status of a specific service**:

```bash
systemctl status <service-name>
```

### 🔹 To check open ports (used services)

```bash
sudo netstat -tulnp
```

or

```bash
sudo ss -tulnp
```

---

## 🪟 **Windows: List All Services**

### 🔹 Using Command Prompt or PowerShell

```powershell
Get-Service
```

* Shows all services and their status (`Running`, `Stopped`).

To list only **running services**:

```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

To list only **stopped services**:

```powershell
Get-Service | Where-Object {$_.Status -eq "Stopped"}
```

### 🔹 Using Task Manager or Services GUI

* Press `Windows + R` → type `services.msc` → Enter.
* Manually browse and filter by `Status` column.

---

Would you like a script to generate a report of active vs inactive services automatically on both OSes?
