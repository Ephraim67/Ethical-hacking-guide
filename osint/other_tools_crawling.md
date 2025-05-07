To **discover files, links, websites, and companies related to a target** using **SpiderFoot** and **theHarvester**, here’s a breakdown of how you can achieve that effectively.



##  **SpiderFoot** (Automated OSINT Framework)

**SpiderFoot** automates many OSINT tasks and integrates with multiple data sources like Shodan, HaveIBeenPwned, VirusTotal, etc. It's ideal for broad reconnaissance.

## Setup:

* Install:

  ```bash
  git clone https://github.com/smicallef/spiderfoot.git
  cd spiderfoot
  pip install -r requirements.txt
  python3 sf.py
  ```
* Or run it in the web UI via: `http://127.0.0.1:5001`



## Use SpiderFoot to Discover:

## **1. Websites & Subdomains**

* Enable modules: `DNS`, `Passive DNS`, `Cert Transparency`, `IP WHOIS`
* Output: Shows subdomains, linked domains, hostnames.

## **2. Files (PDF, DOCX, XLS)**

* Enable: `Web Metadata`, `Web Content`, `Spider`
* It will attempt to **crawl the site** and discover:

  * Links to downloadable files
  * JS/CSS/assets
  * Hidden paths

## **3. Related Companies or Infra**

* Enable modules: `Whois`, `SSL Cert`, `Affiliate`, `Netblocks Owned`
* These help trace the infrastructure owner and related domains.

## **4. External Links**

* From web crawling modules, it will gather:

  * External links (outbound)
  * Related domains linked via analytics/tracking/SSL cert



## Sample Scan Target:

```bash
python3 sf.py -s example.com -o csv -m all
```

You’ll get:

* Subdomains
* Emails
* Linked websites
* Downloadable files
* Infrastructure info



## **theHarvester** (Focused on Emails, Subdomains, Hosts)

**theHarvester** is best for focused reconnaissance on emails, subdomains, hosts, and employee names.

## Setup:

```bash
git clone https://github.com/laramies/theHarvester.git
cd theHarvester
pip install -r requirements.txt
```



## Use theHarvester to Discover:

## **1. Emails and Subdomains**

```bash
python3 theHarvester.py -d example.com -b bing
```

Or use:

```bash
python3 theHarvester.py -d example.com -b google -l 100
```

## **2. Hosts and IPs**

```bash
python3 theHarvester.py -d example.com -b shodan
```

## **3. Combine Sources**

```bash
python3 theHarvester.py -d example.com -b all
```

The `-b` flag accepts sources like:

* `google`, `bing`, `duckduckgo`
* `crtsh` (certificate transparency)
* `shodan`, `hunter`, `anubis`, etc.


## Combine Workflow (SpiderFoot + theHarvester)

| Task                   | Tool         | What it does                            |
| ---------------------- | ------------ | --------------------------------------- |
| Subdomain Discovery    | both         | Crawl DNS, Certs, Search Engines        |
| Discover Files         | SpiderFoot   | Crawls and detects files and metadata   |
| Email Harvesting       | theHarvester | Finds emails via search engines & leaks |
| Infrastructure Mapping | SpiderFoot   | WHOIS, ASN, SSL Cert info               |
| Linked Companies       | SpiderFoot   | Affiliates via shared infra, netblocks  |
| External/Hidden Links  | SpiderFoot   | From crawling & metadata extraction     |

