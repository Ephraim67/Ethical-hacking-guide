Using **Shodan** to search for **CCTV cameras and other IoT devices** is one of its most popular use cases, especially for cybersecurity assessments. Below are **specific queries and techniques** to find **internet-exposed IoT devices**, especially **CCTV**, **webcams**, **routers**, **printers**, and **SCADA/ICS devices**.

---

## 🎯 **Common Shodan Queries for CCTV & IoT Devices**

### 🛑 **Warning:**

These devices are often unsecured. Accessing them **without permission** is illegal and unethical. Use these queries only for **authorized security assessments, research, or educational purposes**.

---

### 📷 **CCTV Cameras / Webcams**

#### 🔎 Network Cameras (Generic)

```sh
title:"Network Camera"
```

#### 📡 Hikvision IP Cameras

```sh
port:80 title:"hikvision" country:"US"
```

#### 📹 Dahua IP Cameras

```sh
port:80 title:"Dahua" country:"US"
```

#### 🔐 Axis Network Cameras (often exposed with open interfaces)

```sh
product:"Axis" port:80
```

#### 🔍 Netwave IP Cameras (many are unprotected)

```sh
title:"Netwave IP Camera"
```

#### 👁️ Webcams with Screenshots

```sh
has_screenshot:true port:80
```

#### 🌐 WebcamXP / WebCam 7

```sh
title:"WebcamXP" OR title:"WebCam 7"
```

---

### 🔌 **Other IoT Devices**

#### 📡 Routers (MikroTik)

```sh
product:"MikroTik RouterOS"
```

#### 🖨️ Printers (HP, Canon, Epson)

```sh
port:80 title:"HP Printer"
```

#### 🔌 Smart Home Devices (TP-Link, Belkin, etc.)

```sh
product:"TP-LINK" OR product:"Belkin"
```

#### 🚨 SCADA/ICS Devices (Critical Infra)

**Use extreme caution with these**

```sh
"modbus" port:502
"siemens" port:102
```

---

## 📁 **Shodan Filters for Precision**

| Filter                | Description                                | Example              |
| --------------------- | ------------------------------------------ | -------------------- |
| `country:`            | Country-specific results                   | `country:"US"`       |
| `city:`               | Devices in a specific city                 | `city:"Lagos"`       |
| `port:`               | Specific open port                         | `port:554`           |
| `org:`                | Organization (ISP/host)                    | `org:"Comcast"`      |
| `net:`                | CIDR range or subnet                       | `net:192.168.1.0/24` |
| `has_screenshot:true` | UI preview if Shodan captured a screenshot |                      |

---

## 🧪 Example Complex Query:

```sh
title:"Network Camera" country:"IN" has_screenshot:true port:80
```

→ Exposed IP cameras in India with a preview image.

---

## 🛠️ Bonus: Use the Shodan CLI

```bash
shodan search 'title:"hikvision" country:"US"'
```

Or use the **Shodan API** in a Python script to automate alerts for new IoT devices appearing in a region.




## Tips to Secure IoT Devices

If you’re assessing your own systems:

* **Change default passwords**
* **Use strong firewall rules**
* **Disable remote access**
* **Use VPNs or NAT**
* **Update firmware**
