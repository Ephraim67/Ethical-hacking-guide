## PROJECT 1: **Automated Threat Hunting and Alerting Pipeline (Using KQL + Sentinel + Logic Apps)**

### Goal:

Create an automated threat detection and response pipeline in Microsoft Sentinel.

### Tasks:

* Build advanced **KQL queries** for:

  * Unusual sign-ins
  * Token replay attacks
  * Impossible travel
  * PowerShell obfuscation
* Configure **analytic rules** and **custom alert tuning**
* Trigger **Microsoft Logic Apps** workflows on alert:

  * Email SOC team
  * Disable user in Entra ID
  * Isolate endpoint via Defender
* Build dashboards showing alert volume, source IPs, MITRE tags.

### Skills Built:

Detection engineering, response automation, KQL mastery, Sentinel workflow logic



## PROJECT 2: **Simulate and Respond to Multi-Stage Attacks (MITRE TTP Mapping)**

### Goal:

Use **Atomic Red Team** to simulate end-to-end attack sequences and build playbooks for response.

### Tasks:

* Choose 2 attack scenarios (e.g., Credential Dumping + Lateral Movement)
* Map steps to MITRE ATT\&CK (e.g., T1003, T1021)
* Simulate on VMs with Defender for Endpoint
* Detect using Defender + Sentinel
* Write playbooks for:

  * Containment (host isolation)
  * Remediation (script/Intune policy to clean)
  * RCA report

### Skills Built:

Threat intelligence, ATT\&CK mapping, blue team playbooks, simulation control


## PROJECT 3: **Security Policy-as-Code with Intune + PowerShell + GPO**

### Goal:

Automate security policy deployment and baseline hardening.

### Tasks:

* Use PowerShell/Graph API to push:

  * BitLocker
  * Application Guard
  * Firewall/Defender configs
* Compare GPO vs Intune enforcement methods
* Use LGPO tool to import/export policies
* Build a Git-based policy repository with version control and change logs

### Skills Built:

Policy automation, Intune scripting, GitOps for security policies



## PROJECT 4: **RBAC Governance and Conditional Access Testing Framework**

### Goal:

Design and validate a zero-trust RBAC model.

### Tasks:

* Define security roles (admin, engineer, contractor)
* Apply **role-based access** with Entra ID + Conditional Access
* Test access from:

  * Compliant device
  * Unmanaged mobile
  * Foreign IP
* Use Defender/MCAS to monitor user behavior
* Write test cases + document expected/actual outcomes

### Skills Built:

Identity governance, zero trust, Conditional Access testing



## PROJECT 5: **Compliance-Driven Security Controls Validation (HIPAA/NIST 800-53)**

### Goal:

Translate HIPAA/NIST controls into testable security policies.

### Tasks:

* Choose 8–10 controls (e.g., AC-6, AU-6, SC-7)
* Create an enforcement strategy:

  * Use Intune, Sentinel, Defender policies
* Write test scripts to validate control presence (e.g., PowerShell scripts)
* Generate compliance audit reports (pass/fail, gap analysis)

### Skills Built:

Compliance integration, control mapping, audit readiness



## Bonus Ideas (Mini Projects)

* **Slack/Teams IR Bot**: Create a bot that pings the SOC when a high-severity Sentinel alert is triggered.
* **Phishing Simulation**: Use GoPhish + Defender to simulate and detect phishing attempts.
* **SIEM Log Forwarder**: Set up NXLog or syslog-NG to ingest Windows/Linux logs into Sentinel for cross-platform visibility.
* **Security Architecture Review**: Diagram and harden an enterprise architecture using Azure security services, firewalls, NSGs, and private endpoints.

