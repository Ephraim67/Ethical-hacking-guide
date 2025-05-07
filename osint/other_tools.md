### 1. **TheHarvester**

* **Purpose**: TheHarvester is an OSINT tool designed to gather emails, domain names, and other related information from various public sources.
* **Features**:

  * Retrieves emails, subdomains, hosts, and banners associated with a domain.
  * Sources include Google, Bing, LinkedIn, and more.
  * Command-line-based and very simple to use.
* **Usage**:

  ```bash
  theharvester -d example.com -b google
  ```
* **Best For**: Quick, straightforward email and domain information gathering.

---

### 2. **Recon-ng**

* **Purpose**: Recon-ng is a powerful web reconnaissance framework that provides a wide range of modules for collecting information about domains, emails, social media, etc.
* **Features**:

  * Supports API integrations (e.g., WhoisXML, Shodan).
  * Comes with a set of built-in modules for finding subdomains, emails, and more.
  * User-friendly interface with a command-line console.
* **Usage**:

  ```bash
  use recon/domains-contacts/whois_pocs
  set SOURCE example.com
  run
  ```
* **Best For**: Structured, modular OSINT collection with integrations.

---

### 3. **Shodan**

* **Purpose**: Shodan is a search engine for internet-connected devices, but it can also be used to gather domain, IP, and service information related to a target.
* **Features**:

  * Find open ports, services, and vulnerabilities.
  * Provides information about the hosting infrastructure and IP addresses linked to the target.
  * Can be integrated with other tools like Maltego.
* **Usage**:

  * Search by domain or IP to retrieve associated devices.
  * Example query: `hostname:"example.com"`.
* **Best For**: Gathering infrastructure details, IP information, and exposed services.

---

### 4. **Have I Been Pwned?**

* **Purpose**: A service that lets you check if an email address has been exposed in any data breaches.
* **Features**:

  * Can be used for checking emails obtained during OSINT.
  * Provides information on breaches and affected websites.
  * API available for automation.
* **Usage**:

  * Search an email directly on the website.
  * Use API to gather breach data programmatically.
* **Best For**: Checking whether discovered emails have been involved in data breaches.

---

### 5. **Hunter.io**

* **Purpose**: Hunter.io is a tool to find and verify email addresses associated with a particular domain.
* **Features**:

  * Provides email addresses linked to specific domains.
  * Offers an email verification tool to check if emails are valid.
  * API available for integration into custom workflows.
* **Usage**:

  * Search for emails related to a domain via the web interface or API.
* **Best For**: Quickly discovering email addresses linked to a domain.

---

### 6. **Censys**

* **Purpose**: Censys provides a search engine for internet-wide scanning of devices and services, including domain and email information.
* **Features**:

  * Collects data on devices, certificates, and domains across the internet.
  * Can search for domain names, IP addresses, and related emails.
  * Provides a rich dataset for deep analysis.
* **Usage**:

  * Search by domain or IP to retrieve related assets and certificates.
* **Best For**: In-depth analysis of internet-wide data for domains and services.

---

### 7. **Amass**

* **Purpose**: Amass is an advanced open-source tool for network mapping and OSINT gathering, focusing on subdomain discovery and related data.
* **Features**:

  * Enumerates subdomains, IP addresses, and domain information.
  * Integrates with multiple data sources like Google, PassiveDNS, Shodan, etc.
  * Can be used for footprinting and network mapping.
* **Usage**:

  ```bash
  amass enum -d example.com
  ```
* **Best For**: Advanced subdomain enumeration and domain mapping.

---

### 8. **DNSdumpster**

* **Purpose**: DNSdumpster is a free online tool that provides DNS information about a domain, including subdomains and mail servers.
* **Features**:

  * Provides DNS information such as MX, A, and CNAME records.
  * Shows associated subdomains.
* **Usage**:

  * Simply input the domain and get results on DNS records, mail servers, and subdomains.
* **Best For**: DNS-based reconnaissance and subdomain discovery.

---

### 9. **Spyse**

* **Purpose**: Spyse is a comprehensive search engine for domain, IP, and asset data.
* **Features**:

  * Offers deep insights into domain ownership, email addresses, and infrastructure.
  * Allows for querying of historical WHOIS data and SSL certificates.
* **Usage**:

  * Use the platform to search for domain or email-based queries.
* **Best For**: Gathering detailed domain and asset information.

---

### 10. **Email Recon (by OSINT Framework)**

* **Purpose**: A collection of tools specifically designed to search for and validate email addresses associated with a domain.
* **Features**:

  * Offers email validation and searching using various OSINT resources.
  * Allows searching for email patterns, social media accounts, and more.
* **Usage**:

  * Search for an email address or domain-related emails.
* **Best For**: Specific email discovery and validation tasks.

---

### 11. **Social Media OSINT Tools**

* **Purpose**: Social media platforms often expose information about individuals and companies, including emails.
* **Examples**: LinkedIn, Twitter, Facebook, and Instagram can be useful for discovering associated emails or contacts tied to specific domains.
* **Best For**: Finding email addresses or personal information indirectly tied to a domain or company.

---

### 12. **Google Dorks**

* **Purpose**: Google Dorks are advanced search queries that can help find hidden information on the web, including emails, files, and domain information.
* **Examples**:

  * `site:example.com inurl:email`
  * `site:example.com filetype:pdf`
* **Best For**: Discovering hidden documents or email addresses on a domain.

---

### 13. **Passive DNS**

* **Purpose**: Passive DNS data provides historical and current DNS query information, helping to identify subdomains, mail servers, and associated infrastructure.
* **Services**:

  * PassiveTotal
  * Farsight Security
* **Best For**: Subdomain enumeration and DNS-based analysis.



These tools, when combined effectively, can provide a comprehensive view of domain information and associated emails. Each tool has its strengths:

* **Maltego** and **Recon-ng** are great for structured reconnaissance.
* **TheHarvester** and **Amass** excel at domain and subdomain enumeration.
* **Hunter.io** and **Have I Been Pwned** are ideal for finding emails and checking their security status.

