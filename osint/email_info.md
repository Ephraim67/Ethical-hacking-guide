Using **Maltego** to discover **domain information** and **associated emails** with a target is a common reconnaissance technique in cybersecurity and OSINT (Open Source Intelligence). Here's a step-by-step guide to help you do that effectively:


### **Tools Needed:**

* **Maltego Desktop Application** (Community or Pro version)
* **Internet connection**
* Optional: **Maltego Transforms** API keys (for better results using services like Shodan, HaveIBeenPwned, WhoisXML, etc.)



### **Step-by-Step Process:**

#### 1. **Create a New Graph in Maltego**

* Launch Maltego and create a new graph.
* Select the **Entity Type**: Start with a `Domain` entity (e.g., `example.com`).

#### 2. **Discover Domain Information**

* Right-click the Domain entity → Choose transforms under **"Infrastructure"**:

  * `To DNS Name – MX` (Mail servers)
  * `To DNS Name – NS` (Name servers)
  * `To IP Address`
  * `To Website`

This helps identify:

* Hosting infrastructure
* Related IPs and subdomains
* Mail servers (can hint at internal IT structure)

#### 3. **Enumerate Subdomains**

* Run:

  * `To DNS Name [using Search Engine]`
  * `To Domain – from whois information`
  * Use transforms from **Farsight DNSDB**, **PassiveTotal**, or **VirusTotal** (if available)

#### 4. **Find Associated Email Addresses**

* Right-click the domain or subdomains → Use transforms under **“Email Addresses”**:

  * `To Email Address [From whois information]`
  * `To Email Address [search engine]`
  * If you have the **HaveIBeenPwned** API key, you can also check if emails have been involved in breaches.
  * `To Person` or `To Social Media Profiles` transforms can help trace email identities.

#### 5. **Pivot from Emails to More Data**

* After finding email addresses, right-click and pivot:

  * `To Domain`
  * `To Person`
  * `To Phone Number`
  * `To Location`
  * `To Company`

This may uncover internal contacts, employees, and external links.

#### 6. **Correlate and Visualize**

* Use Maltego’s graph to see how emails relate to subdomains, IPs, or other entities.
* Use filters to hide irrelevant data and focus on useful links.


* Use **Shodan transforms** to get IoT devices or open services.
* Use **WHOISXML** for richer WHOIS data.
* Install **Maltego's OSINT Hub** transforms (free and paid).
* Combine this with **manual searches** in Hunter.io, Google Dorks, or LinkedIn scraping for better coverage.
