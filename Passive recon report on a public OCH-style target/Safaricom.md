# Safaricom PLC – Passive OSINT Attack Surface Reconnaissance Report

**Target:** Safaricom PLC (Kenya’s leading mobile network operator and fintech provider via M-Pesa)

**Public Bug Bounty / Disclosure Policy:**
https://hackerone.com/safaricom?type=team

---

# 1. Write-Up & Methodology Overview

This report outlines a strictly passive Open Source Intelligence (OSINT) reconnaissance of Safaricom. No active packets were sent to Safaricom infrastructure during the assessment. Activities such as port scanning, header probing, service enumeration, banner grabbing, or direct interaction with production systems were intentionally avoided.

The objective was to map the external attack surface by aggregating publicly available information from third-party sources that already index or reference Safaricom's digital footprint.

## Trade-Offs Made

### Passive vs. Active Reconnaissance

By avoiding active scanning techniques, the assessment minimizes operational noise and avoids potential fingerprinting by target defenses. However, reliance on publicly indexed information means some ephemeral or recently deployed services may not be visible if they have not been captured by external observers.

### Security Disclosure Channel Identification

The endpoint:

```
https://safaricom.com/.well-known/security.txt
```

returned a 404 or inaccessible response.

Rather than assuming the absence of a vulnerability disclosure process, the corporate website was reviewed for equivalent security reporting mechanisms. The Security Incident Reporting page was identified as the authoritative disclosure channel.

### Scope Definition

Safaricom operates a large and diverse technology ecosystem. This assessment focuses primarily on publicly exposed web-facing assets including:

* Marketing websites
* Customer support portals
* Developer platforms
* Public-facing service endpoints

Internal BSS/OSS systems and backend infrastructure were not examined beyond references found through public records.

---

# 2. OSINT Source Classes Consulted

To build a comprehensive external attack surface inventory, multiple passive intelligence sources were consulted.

## Web Archive & DNS History

Historical snapshots and DNS records were reviewed to identify legacy services, retired infrastructure, and previously exposed subdomains.

### Tools / Methods

* Wayback Machine (`web.archive.org`)
* WhoisXML API
* Public DNS history aggregators

---

## Developer Ecosystem Monitoring

Developer communities and public repositories were reviewed for references to Safaricom services, APIs, integrations, and technical implementations.

### Tools / Methods

* GitHub search
* GitLab search
* Stack Overflow
* Search engine indexing of developer resources

---

## SSL/TLS Certificate Transparency Logs

Certificate Transparency Logs were analyzed to enumerate domains and subdomains associated with Safaricom certificates.

### Tools / Methods

* crt.sh
* Public CT log aggregators

---

## Third-Party SaaS & Service Footprints

Vendor integrations and externally hosted services were identified through publicly available records and archived content.

### Tools / Methods

* Passive subdomain enumeration
* HTML source inspection from archived pages
* CDN and cloud service footprint analysis

---

# 3. External Surface Inventory

Based on Certificate Transparency records, archived DNS information, and historical web content, Safaricom maintains a significant externally accessible digital footprint.

## Estimated Exposure

* Approximately 40–60+ unique subdomains identified from recent CT logs and archived records.
* Includes both active and recently observed assets.
* Historical redirects and retired infrastructure excluded where possible.

## Categories Observed

* Marketing portals
* Developer API platforms
* Customer support services
* Mobile application gateways
* Partner integration endpoints

## Notable Examples

### developer.safaricom.co.ke

Primary hub for the Daraja developer platform.

Observed functionality:

* API documentation
* Authentication workflows
* M-Pesa integration guidance
* Sample code repositories

---

### mpesa.co.ke / m.pesa.com

Brand-specific domains associated with M-Pesa services.

Observed functionality:

* Product information
* Customer-facing services
* Partner integration resources

---

### careers.safaricom.co.ke

Recruitment and employment platform.

Observed functionality:

* Job listings
* Technical hiring information
* Technology stack references in vacancy descriptions

---

# 4. Key Findings & Impact Assessment

The following findings represent areas that warrant further review by the security team.

---

## Finding #1: High-Value Developer Portal Exposure

### Observation

The developer portal (`developer.safaricom.co.ke`) contains extensive documentation related to M-Pesa and Daraja APIs, including:

* OAuth workflows
* Webhook integrations
* API request examples
* Sample application code

### Impact Reasoning

Developer platforms naturally expose implementation details that can assist legitimate integrators. However, they also provide attackers with insight into:

* Authentication workflows
* Callback mechanisms
* Token management processes
* Expected request structures

Any weaknesses in webhook validation or API authorization controls could increase risk to connected financial ecosystems.

---

## Finding #2: Potential Legacy Widget Security Risk

### Observation

Archived versions of support and recruitment portals contain evidence of embedded third-party widgets such as:

* Customer support chat systems
* Helpdesk integrations
* Marketing engagement tools

Examples were observed on:

* careers.safaricom.co.ke
* support-related web properties

### Impact Reasoning

Legacy third-party components can introduce security risks if they:

* Process user-supplied content
* Lack modern Content Security Policies (CSP)
* Remain connected to deprecated back-end services

Potential outcomes may include Stored XSS or other client-side injection issues affecting authenticated users.

---

## Finding #3: Potential Subdomain Takeover Risk

### Observation

Historical DNS records suggest some subdomains previously pointed to external SaaS providers, including:

* Cloud hosting services
* Content delivery networks
* Static site platforms

Examples include services commonly hosted on:

* AWS CloudFront
* GitHub Pages
* Other managed SaaS providers

### Impact Reasoning

If DNS records remain active after associated services are decommissioned, an attacker may be able to claim the abandoned resource and gain control of the affected subdomain.

Potential consequences include:

* Phishing campaigns
* Brand impersonation
* Malicious content hosting
* Abuse of trusted subdomains

---

# 5. Activities Explicitly Not Performed

To maintain a strictly passive reconnaissance approach, the following activities were intentionally excluded.

## No Port Scanning

Tools such as:

* Nmap
* Masscan
* RustScan

were not used against Safaricom-owned IP ranges.

### Reason

Avoids direct interaction with target infrastructure and prevents generation of security monitoring events.

---

## No Live HTTP Header Analysis

No direct requests were made using tools such as:

* curl
* Postman
* Burp Suite

for the purpose of collecting:

* Security headers
* Cookie attributes
* Server banners

### Reason

Preserves passive methodology and avoids triggering WAF, IDS, or logging systems.

---

## Limited Deep Content Crawling

The assessment focused on top-level content and publicly indexed information.

### Reason

Avoids extensive automated collection of website content while still providing a representative view of the external attack surface.

---

# Conclusion

This passive OSINT assessment identified a substantial public-facing attack surface associated with Safaricom's web ecosystem. Developer platforms, legacy third-party integrations, and historical DNS records represent the most notable areas for continued security review.

The findings should be treated as reconnaissance indicators requiring validation through authorized security testing before any vulnerability claims are made.
