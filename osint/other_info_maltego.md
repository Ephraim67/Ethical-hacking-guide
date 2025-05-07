To **discover files, links, websites, and companies related to a target** using **Maltego**, you can follow a structured process using various **Maltego entities** and **transforms**. Here's how to carry out this investigation:


## **GOAL:**

Find publicly available **files (docs, PDFs)**, **external/internal links**, **related websites**, and **company relationships** tied to a **target (domain, company, person, etc.)**



## **1. Start with a Known Entity**

Common starting points:

* `Domain` (e.g., `example.com`)
* `Company` (e.g., `Example Ltd`)
* `Website` (e.g., `www.example.com`)
* `Person` or `Email address` (if you have that)



## **2. Discover Related Links and Websites**

**From a Domain or Website entity**:

* Right-click → Run transforms:

  * `To Website [Quick Lookup]`
  * `To DNS Name`
  * `To IP Address`
  * `To Website using Google`
  * `To Other Sites Hosted on Same IP`
  * `To Domains Sharing Same Analytics Code` (useful to find linked companies or websites)
  * `To Entities using Same SSL Cert` (helps detect shared infrastructure)

> Repeat this step with newly found domains or IPs to widen your scope.



## **3. Discover Publicly Available Files (Documents)**

**From a Domain entity**:

* Use search engine transforms:

  * `To URL [Using Search Engine]` → searches indexed links
  * `To Documents [filetype:pdf|docx|xls using search engine]`
* Example transforms:

  * `To URL (Filetype Search - PDF)`
  * `To URL (Filetype Search - DOCX)`
  * `To URL (Filetype Search - XLSX)`

> These leverage Google/Bing dorks behind the scenes (e.g., `site:example.com filetype:pdf`)

You can then:

* Analyze metadata of documents (e.g., using FOCA or external tools).
* Pivot from discovered author names or emails inside metadata.


## **4. Identify Linked Companies or Subsidiaries**

**From a Company entity**:

* Run transforms like:

  * `To Domain`
  * `To Affiliate Companies`
  * `To Owned Companies`
  * `To Parent Organization`

**From domains/IPs/websites**:

* Use:

  * `To Company [from WHOIS data]`
  * `To Company [based on SSL cert]`
  * `To Organizations [Linked via Shared Infrastructure]`

These help detect:

* Other domains/brands owned by same company
* Subsidiary or partner companies



## **5. Crawl and Map Website Links**

**From a Website entity**:

* Use:

  * `To URLs [Crawl Web Pages]` (requires API or specific transforms)
  * `To External Links`
  * `To Internal Links`
  * `To Linked Files (scripts, documents, media)`

Note: Maltego is not a full web crawler, but with proper transforms (like **Spiderfoot integration**, or custom API-based crawlers), it can partially crawl link structures.



## **6. Correlate External Resources**

From a website or domain:

* `To WHOIS info → To Email → To Company`
* `To Social Media Accounts`
* `To Hosting Providers`

These help correlate:

* External services
* Developer accounts
* Hosting infrastructure



## **7. Use Third-Party Transform Integrations**

Consider installing or activating:

* **Farsight DNSDB**
* **HaveIBeenPwned**
* **VirusTotal**
* **Shodan**
* **BuiltWith** (detects technologies used by websites)
* **SSL Cert transforms** (find related domains using same cert)



**Use the graph layout tools** in Maltego:

* Group related domains/websites
* Filter by filetype, email domain, or company
* Use views like Entity List or Ball Size to see high-value nodes
