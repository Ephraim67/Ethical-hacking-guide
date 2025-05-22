Here are some effective **OSINT (Open Source Intelligence)** tools and techniques you can use to find **email addresses** of people working within a company:

---

### 🔍 **1. Google Dorking**

Use search operators to find exposed emails:

```
site:company.com "@company.com"
site:company.com "email"
site:linkedin.com/in "company name" AND "@company.com"
```

---

### 🧰 **2. Hunter.io**

* URL: [https://hunter.io](https://hunter.io)
* **Function**: Finds email addresses associated with a domain.
* **Bonus**: Shows email patterns (e.g., `{first}.{last}@company.com`), and sources where it was found.

---

### 🧰 **3. Email Permutator+**

* URL: [https://metricsparrow.com/toolkit/email-permutator/](https://metricsparrow.com/toolkit/email-permutator/)
* **Function**: Generates possible email permutations based on name and domain.
* **Use With**: Tools like Hunter.io or verify with Email Verifier tools.

---

### 🧰 **4. LinkedIn + SalesQL / Lusha / Skrapp**

* LinkedIn is a goldmine for identifying people at a company.
* **Tools**:

  * [SalesQL](https://salesql.com)
  * [Lusha](https://www.lusha.com)
  * [Skrapp](https://skrapp.io)
* These browser extensions often find business emails and export them to CSV.

---

### 🧰 **5. VoilaNorbert**

* URL: [https://www.voilanorbert.com/](https://www.voilanorbert.com/)
* **Function**: Email guessing and verification tool.
* Input name + domain, get possible and verified emails.

---

### 🧰 **6. Hunter Email Verifier / Verify Email Address**

* Hunter has a built-in verifier.
* You can also use:

  * [https://email-checker.net](https://email-checker.net)
  * [https://verify-email.org](https://verify-email.org)

---

### 🧰 **7. theHarvester (Kali Linux tool)**

* CLI OSINT tool to gather emails, subdomains, and more.
* Usage:

  ```bash
  theHarvester -d company.com -b google
  ```

---

### 🧰 **8. Snusbase / IntelX / Dehashed**

* Search historical data breaches for company email addresses:

  * [https://intelx.io](https://intelx.io)
  * [https://snusbase.com](https://snusbase.com)
  * [https://dehashed.com](https://dehashed.com)

---

### 🧰 **9. GitHub & Pastebin Search**

Search for leaked credentials or internal emails in code/pastes:

```
site:github.com "@company.com"
site:pastebin.com "@company.com"
```

---

### 🧰 **10. Maltego (with plugins)**

* Advanced graphical OSINT tool.
* Use plugins to integrate with HaveIBeenPwned, Hunter, or Whois XML APIs to gather emails.

---

### 🧪 Bonus: Create a Target Profile

Use tools like:

* **SpiderFoot**
* **Recon-ng**
* To automate discovery of emails from multiple sources.

---

If you want a **complete recon workflow** or automated script for this, let me know and I’ll prepare one.
