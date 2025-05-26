## ✅ **Module Objectives**

By the end of the module, students will be able to:

1. Configure a secure baseline for Linux and Windows systems.
2. Understand and apply patch management and vulnerability assessment.
3. Explain the secure development lifecycle (SDLC).
4. Identify and mitigate OWASP Top 10 vulnerabilities.
5. Perform hands-on vulnerability scans and web app penetration tests.



##  **Session Breakdown**

###  **Session 1: OS Hardening & Secure Configuration**

**Objectives:**

* Learn best practices for securing operating systems.
* Apply secure configuration to Windows and Linux.

**Topics:**

* Disable unnecessary services.
* Configure firewalls (UFW, Windows Defender).
* Enforce strong password policies.
* Enable logging/auditing.

**Tools:**

* Linux terminal (Ubuntu/Kali)
* Windows VM
* `auditd`, `ufw`, Group Policy Editor

**Activity:**

* Students secure a Linux and Windows VM using a checklist.



###  **Session 2: Patch Management & Vulnerability Scans**

**Objectives:**

* Understand why patching is critical.
* Perform vulnerability assessments using scanning tools.

**Topics:**

* Patch management tools: `apt`, `yum`, WSUS
* Introduction to CVEs, CVSS
* Automated scanning tools: Nessus, OpenVAS

**Lab:**

* Launch Nessus/OpenVAS on a test network
* Scan a vulnerable VM (e.g., Metasploitable)

**Deliverable:**

* Vulnerability report and remediation suggestions


###  **Session 3: Secure Development Lifecycle (SDLC)**

**Objectives:**

* Learn how security is integrated into software development.

**Topics:**

* Phases: Requirements → Design → Implementation → Testing → Maintenance
* Secure coding practices
* Threat modeling basics (e.g., STRIDE)

**Activity:**

* Analyze a sample SDLC flow and identify where security can be injected.



###  **Session 4: OWASP Top 10 & Application Security**

**Objectives:**

* Identify common web app vulnerabilities.
* Use OWASP ZAP to test and secure web applications.

**Topics:**

* OWASP Top 10 (Injection, XSS, Broken Auth, etc.)
* Testing tools: OWASP ZAP, Burp Suite (optional)

**Lab:**

* Test a deliberately vulnerable web app (e.g., Juice Shop or DVWA) with OWASP ZAP.

**Deliverable:**

* Report on discovered vulnerabilities and how to mitigate them.


##  **Lab Setup Checklist**

| Tool                  | Purpose                    | Setup Notes                      |
| --------------------- | -------------------------- | -------------------------------- |
| **Nessus** / OpenVAS  | Vulnerability scanning     | Install on Kali or standalone VM |
| **OWASP ZAP**         | Web app testing            | Pre-installed on Kali Linux      |
| **DVWA / Juice Shop** | Vulnerable app             | Run on localhost or Docker       |
| **Metasploitable 2**  | Vulnerable OS for scanning | VirtualBox or VMware             |



##  Assessment Methods

* **Quizzes** on hardening and OWASP topics.
* **Lab reports** with screenshots and summaries.
* **Group project**: Harden a system and present findings.



##  Optional Resources

* [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks) for secure configuration
* OWASP Juice Shop: [https://owasp.org/www-project-juice-shop/](https://owasp.org/www-project-juice-shop/)
* SDLC Overview: [https://owasp.org/www-project-secure-software-development-lifecycle/](https://owasp.org/www-project-secure-software-development-lifecycle/)
