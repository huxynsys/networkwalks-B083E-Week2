# PENETRATION TESTING REPORT 
### Footprinting & Network Scanning Phases

**W2-PM-FINAL  |  CYBERSECURITY  |  NETWORKWALKS**

| Field | Detail |
|---|---|
| **Pentester Name (Cybersecurity Professional)** | **Lal Hussain** |
| **Program/Batch** | B083E-Networkwalks |
| **Date** | 18 September 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools)<br>W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (secured written permission already)<br>2. My own local LAN Network |
| **Permission secured from client?** | Yes |
| **Phases covered** | **Phase 1:** Reconnaissance & Footprinting<br>**Phase 2:** Scanning & Network Discovery<br>**Phase 3-5:** In Progress |

# 1. Liability Disclaimer

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

# 2. Introduction

This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5). One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks.

All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed (scanning). Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.

# 3. Activities Performed

## 3.1 Footprinting & Reconnaissance

# 🔐 Networkwalks — Web Reconnaissance Report


## 📌 1. Introduction

This project documents the **footprinting and reconnaissance activities** performed during the Cybersecurity & Ethical Hacking internship.

The objective of this practical exercise was to understand how security professionals gather information about a target before performing deeper security testing.

The authorized target used for the exercise was:

```text
networkwalks.com
```

The assessment focused on collecting publicly observable information related to:

* Domain registration
* DNS infrastructure
* IP addressing
* Web technologies
* HTTP response headers
* Web Application Firewall (WAF)
* Mail and DNS records

No exploitation or destructive testing was performed.

> ⚠️ **Authorization Notice:**
> All activities documented in this report were performed as part of an authorized educational cybersecurity exercise. Reconnaissance and scanning should only be performed against systems for which appropriate permission has been provided.

---

# 🎯 2. Objectives

The main objectives of this practical exercise were:

1. Understand the purpose of cybersecurity footprinting.
2. Collect publicly available information about a target domain.
3. Identify DNS and network information.
4. Fingerprint web technologies.
5. Analyze HTTP response headers.
6. Identify the presence of a Web Application Firewall.
7. Enumerate available DNS records.
8. Document findings in a structured security report.
9. Understand the difference between an observation and a confirmed vulnerability.

---

# 🛠️ 3. Tools Used

The following Kali Linux tools were used during the reconnaissance exercise:

| Tool       | Purpose                                       |
| ---------- | --------------------------------------------- |
| `whois`    | Domain registration and ownership information |
| `whatweb`  | Web technology fingerprinting                 |
| `nslookup` | DNS resolution and IP identification          |
| `curl`     | HTTP response and header analysis             |
| `wafw00f`  | Web Application Firewall detection            |
| `dnsrecon` | DNS record enumeration                        |

---

# 🔎 4. Methodology

The assessment followed a basic reconnaissance methodology.

### Phase 1 — Domain Information Gathering

WHOIS was used to collect domain registration information such as:

* Registrar
* Creation date
* Expiration date
* Nameservers
* Domain status
* DNSSEC status

### Phase 2 — Web Technology Fingerprinting

WhatWeb was used to identify technologies exposed by the website, including:

* Web server
* CMS
* JavaScript libraries
* Web frameworks
* Plugins and other technologies

### Phase 3 — DNS Resolution

Nslookup was used to determine the IP address associated with the target domain.

### Phase 4 — HTTP Analysis

Curl was used to inspect HTTP response headers and identify additional technical information exposed by the web server.

### Phase 5 — WAF Detection

Wafw00f was used to determine whether the target was protected by a Web Application Firewall.

### Phase 6 — DNS Enumeration

DNSRecon was used to identify additional DNS records, including:

* SOA
* NS
* A
* MX
* TXT
* SRV

---

# 3.1.1 WHOIS Enumeration

### Command

```bash
whois networkwalks.com
```

### Key Findings

The WHOIS lookup provided the following information:

| Attribute       | Finding                |
| --------------- | ---------------------- |
| Domain          | `networkwalks.com`     |
| Registrar       | GoDaddy.com, LLC       |
| Creation Date   | `2019-11-06`           |
| Registry Expiry | `2027-11-06`           |
| DNSSEC          | Unsigned               |
| Nameserver 1    | `ns6135.hostgator.com` |
| Nameserver 2    | `ns6136.hostgator.com` |

The registrant information was privacy protected through **Domains By Proxy, LLC**.

### Security Relevance

WHOIS information can help establish an initial understanding of a domain's registration and DNS infrastructure.

It may provide useful information for:

* Asset identification
* Infrastructure mapping
* Security assessment preparation
* Domain ownership verification

The information itself does not represent a vulnerability.

---

# 3.1.2 Web Technology Fingerprinting

### Command

```bash
whatweb networkwalks.com
```

### Key Findings

WhatWeb identified several technologies associated with the website:

| Technology                 | Observation |
| -------------------------- | ----------- |
| Web Server                 | Apache      |
| CMS                        | WordPress   |
| WordPress Download Manager | `3.3.58`    |
| jQuery                     | `3.7.1`     |
| Bootstrap                  | `7.1.1`     |
| Google Tag Manager         | Detected    |
| HTML5                      | Detected    |
| Open Graph Protocol        | Detected    |

The page title was:

```text
Networkwalks Academy
```

The target resolved to:

```text
192.232.216.135
```

The HTTP version redirected to HTTPS, while the HTTPS version returned:

```text
200 OK
```

### Security Relevance

Technology fingerprinting can help security professionals understand the technologies forming part of an application's attack surface.

For example, identifying a CMS or plugin version allows authorized testers to determine whether those components require further security review.

However:

> **Identifying a software version does not confirm that the software is vulnerable.**

---

# 3.1.3 DNS Resolution

### Command

```bash
nslookup networkwalks.com
```

### Result

```text
Name:    networkwalks.com
Address: 192.232.216.135
```

The domain resolved to:

```text
192.232.216.135
```

The DNS server used for the lookup was:

```text
192.168.100.1
```

The response was identified as non-authoritative.

### Security Relevance

DNS resolution is an important part of reconnaissance because it allows a security professional to associate a domain name with an IP address.

This information can be used as a starting point for authorized infrastructure assessment.

---

# 3.1.4 HTTP Header Analysis

### Command

```bash
curl -I https://networkwalks.com
```

### Response

The target returned:

```text
HTTP/2 200
```

The response identified:

```text
server: Apache
```

Other observations included:

```text
content-type: text/html; charset=UTF-8
referrer-policy: no-referrer-when-downgrade
x-endurance-cache-level: 0
x-nginx-cache: WordPress
```

The response also exposed a WordPress REST API reference:

```text
https://networkwalks.com/wp-json/
```

and a WordPress page API reference:

```text
https://networkwalks.com/wp-json/wp/v2/pages/53
```

### Security Relevance

HTTP headers can provide useful information about:

* Web server technology
* Application technology
* Security policies
* Caching
* API endpoints
* Application behavior

This information can contribute to technology fingerprinting and attack-surface mapping.

The presence of a WordPress REST API endpoint alone does not indicate a vulnerability.

---

# 3.1.5 WAF Detection

### Command

```bash
wafw00f networkwalks.com
```

### Result

Wafw00f identified:

```text
The site https://networkwalks.com is behind ModSecurity (SpiderLabs) WAF.
```

### Finding

The target was identified as being behind:

```text
ModSecurity (SpiderLabs)
```

### Security Relevance

A Web Application Firewall can inspect HTTP requests and apply security rules before requests reach the underlying web application.

During reconnaissance, identifying a WAF is useful because it provides information about the security architecture of the target.

> The Wafw00f result confirms WAF detection, but this exercise did not test whether the WAF successfully blocks specific attacks.

---

# 3.1.6 DNS Enumeration

### Command

```bash
dnsrecon -d networkwalks.com
```

DNSRecon identified multiple DNS records.

### SOA Record

```text
ns6135.hostgator.com
50.87.144.87
```

### Nameservers

```text
ns6135.hostgator.com
ns6136.hostgator.com
```

### Nameserver IP

One nameserver resolved to:

```text
ns6136.hostgator.com → 192.232.216.131
```

The other resolved to:

```text
ns6135.hostgator.com → 50.87.144.87
```

### DNS Server Version

DNSRecon reported:

```text
BIND 9.16.23-RH
```

### A Record

```text
networkwalks.com → 192.232.216.135
```

### MX Record

```text
mail.networkwalks.com → 192.232.216.135
```

### TXT Records

An SPF record was identified:

```text
v=spf1 +a +mx +ip4:50.87.144.87 +include:websitewelcome.com ~all
```

A Google site-verification TXT record was also identified.

### SRV Records

Multiple `_autodiscover._tcp` records were identified pointing to:

```text
cpanelemaildiscovery.cpanel.net
```

### DNSSEC

DNSRecon reported:

```text
ERROR No answer for DNSSEC query for networkwalks.com
```

This was consistent with the WHOIS result indicating:

```text
DNSSEC: unsigned
```

### Security Relevance

DNS enumeration can reveal information about:

* Hosting infrastructure
* Mail infrastructure
* Nameservers
* Service discovery
* Domain configuration

This information can help build a broader infrastructure profile during an authorized security assessment.

---

# 📊 3.1.7 Reconnaissance Summary

| Category            | Finding                  |
| ------------------- | ------------------------ |
| Target Domain       | `networkwalks.com`       |
| Public IP           | `192.232.216.135`        |
| Registrar           | GoDaddy.com, LLC         |
| Nameservers         | HostGator                |
| Web Server          | Apache                   |
| CMS                 | WordPress                |
| WP Download Manager | `3.3.58`                 |
| jQuery              | `3.7.1`                  |
| Bootstrap           | `7.1.1`                  |
| WAF                 | ModSecurity (SpiderLabs) |
| DNSSEC              | Unsigned                 |
| MX Record           | `mail.networkwalks.com`  |
| SPF                 | Present                  |
| REST API            | `/wp-json/` observed     |
| HTTPS               | Enabled                  |
| HTTP → HTTPS        | Redirect observed        |

---

# ⚠️ 5. Risk Analysis / Impact

Based on the information collected during the footprinting and reconnaissance activities, the following **potential risks and observations** were identified.

| # | Risk / Finding                         | Evidence / Observation                                                   | Potential Impact                                                                                  | Risk Level   |
| - | -------------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------- | ------------ |
| 1 | Web technology information exposed     | WhatWeb identified WordPress, WP Download Manager and other technologies | Attackers may use technology information to identify components requiring further security review | **● Medium** |
| 2 | Server IP address identifiable         | Nslookup resolved the domain to `192.232.216.135`                        | Provides information about the network location of the web service                                | **● Low**    |
| 3 | HTTP technical information exposed     | Curl returned HTTP headers and exposed `/wp-json/` references            | May assist technology fingerprinting and further enumeration                                      | **● Low**    |
| 4 | WAF technology identifiable            | Wafw00f identified ModSecurity (SpiderLabs)                              | Reveals information about the web application's security architecture                             | **● Low**    |
| 5 | DNS infrastructure information exposed | DNSRecon identified DNS, mail, TXT and service-related records           | Can help build a broader infrastructure profile                                                   | **● Medium** |
| 6 | DNSSEC not enabled                     | WHOIS reported DNSSEC as unsigned and DNSRecon returned no DNSSEC answer | DNS responses are not protected by DNSSEC validation for this domain                              | **● Low**    |

### Risk Level Key

```text
● Critical
● High
● Medium
● Low
```

> **Important:** The findings above are reconnaissance observations and potential risks, not confirmed vulnerabilities.

The practical exercise primarily involved information gathering. No exploitation or vulnerability validation was performed.

Therefore, the presence of a software version, IP address, DNS record, API endpoint or WAF does not by itself prove that the system is vulnerable.

Further authorized security testing would be required to confirm any actual vulnerability.

---

# 🛡️ 6. Recommendations

Based on the observations from the reconnaissance activities, the following security improvements are recommended.

### 1. Review Publicly Exposed Technology Information

Organizations should periodically review what information about their:

* CMS
* Plugins
* Frameworks
* Libraries
* Web servers

is publicly exposed.

Where practical, unnecessary version information should not be unnecessarily disclosed.

---

### 2. Keep Software Updated

WordPress, plugins, libraries and other web technologies should be regularly updated.

Organizations should also monitor relevant security advisories and review installed components for known vulnerabilities.

---

### 3. Review HTTP Response Headers

HTTP response headers should be reviewed periodically to determine whether unnecessary technical information is being exposed.

Security-related headers should also be configured appropriately according to the application's requirements.

---

### 4. Review DNS Records

DNS records should be reviewed regularly to ensure that:

* Only required records are publicly available.
* Old records are removed.
* Unused services are not unnecessarily exposed.
* Mail and service records are correctly configured.

---

### 5. Properly Configure and Monitor the WAF

The detected ModSecurity WAF should be:

* Kept updated
* Properly configured
* Regularly monitored
* Tested using authorized security assessments
* Reviewed for false positives and false negatives

The WAF should be considered one layer of defense rather than a replacement for secure application development.

---

### 6. Consider DNSSEC Deployment

Where appropriate for the organization's requirements, DNSSEC should be evaluated to provide authentication of DNS responses and help protect against certain DNS-related attacks.

---

### 7. Maintain an Asset Inventory

Organizations should maintain an accurate inventory of:

* Domains
* IP addresses
* Servers
* Applications
* DNS records
* Third-party services

This makes it easier to identify unexpected or forgotten assets.

---

### 8. Perform Regular Security Assessments

Authorized security assessments should be performed periodically to identify weaknesses that cannot be determined through basic reconnaissance alone.

---

### 9. Perform Testing Only Within an Authorized Scope

Reconnaissance, scanning and vulnerability testing should only be performed against systems and networks where appropriate authorization has been provided.

---

# 🧪 7. Scope and Limitations

The activities documented in this report were limited to **footprinting, reconnaissance and information gathering**.

The assessment did not include:

* Exploitation
* Password attacks
* Brute-force attacks
* Denial-of-service testing
* Destructive testing
* Unauthorized access
* Data modification
* Malware deployment

Because exploitation and vulnerability validation were outside the scope of this exercise, the findings should not be interpreted as confirmed vulnerabilities.

The results represent the information observable during the time of testing.

---



# 📸 Recommended Screenshots

For the GitHub project documentation, include screenshots of the following terminal outputs:

### Screenshot 1 — WHOIS

Show:
<img width="1016" height="456" alt="image" src="https://github.com/user-attachments/assets/947f04d4-2991-4f1b-ab4b-fbfc2756b7f8" />



### Screenshot 2 — WhatWeb

Show:
<img width="1143" height="252" alt="image" src="https://github.com/user-attachments/assets/e53afaf0-e270-4760-96a1-1e16b90ab608" />


### Screenshot 3 — DNS Resolution

Show:
<img width="361" height="153" alt="image" src="https://github.com/user-attachments/assets/71520162-a4fe-4af9-9c55-4dfde0d49eaa" />




### Screenshot 4 — HTTP Headers

Show:

<img width="1145" height="246" alt="image" src="https://github.com/user-attachments/assets/43aeac48-eed5-4a0b-a0ba-97d405bcb5bf" />


### Screenshot 5 — WAF Detection

Show:

<img width="768" height="325" alt="image" src="https://github.com/user-attachments/assets/6f74af02-2c96-4007-91ff-71af7ada917f" />


### Screenshot 6 — DNSRecon

Show:

<img width="1087" height="425" alt="image" src="https://github.com/user-attachments/assets/8705b7be-8eee-495e-9415-eaea0bbcb8ca" />




# 📝 Conclusion

The reconnaissance phase successfully established a baseline understanding of the `networkwalks.com` infrastructure.

The assessment identified the domain's registration information, DNS infrastructure, public IP address, web server, WordPress installation, additional web technologies, HTTP headers, email-related DNS records, and the presence of a ModSecurity WAF.

These findings provide the foundation for further **authorized security assessment and vulnerability analysis**.

> **Important:** The presence of a technology, service, API endpoint, or configuration does not by itself demonstrate a security vulnerability. Further authorized validation would be required before classifying any item as a vulnerability.

---

## 👨‍💻 Skills Demonstrated

* Web Reconnaissance
* OSINT Fundamentals
* WHOIS Enumeration
* DNS Enumeration
* DNS Record Analysis
* Web Technology Fingerprinting
* HTTP Header Analysis
* WAF Detection
* Attack Surface Identification
* Linux/Kali Linux Command-Line Usage

---

## ⚖️ Disclaimer

This project was completed for **educational and authorized cybersecurity training purposes**.

All reconnaissance activities should only be performed against systems for which you have explicit permission to conduct security testing.

## 3.2 Network Scanning with Zenmap

For the second activity, I used **Zenmap** to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.

I first used the Windows `ipconfig` command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected **Ping Scan** to identify active hosts.

the identified four live hosts:

- `192.168.100.1`
- `192.168.100.3`
- `192.168.100.11`
- `192.168.100.35`



After completing the scan, I opened the **Topology** section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.

**Note:** The actual subnet, number of hosts and addresses should be replaced with the results from my own network when submitting the report.


# 4. Conclusion

During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.

In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.

In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology.

The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.

I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.

Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as part of the assigned educational cybersecurity lab.



-End-
