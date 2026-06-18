# Netflix Passive OSINT Reconnaissance Report


# Scope and Authorisation

**Target:** Netflix

**Authorisation:** Publicly available assets listed under the Netflix HackerOne bug bounty program.

## Methodology

- Passive reconnaissance only
- No active scanning performed
- No fuzzing performed
- No authentication attempts performed
- No brute forcing performed
- No interaction beyond publicly available information

## Sources Used

- HackerOne
- crt.sh
- Censys
- FOFA
- BuiltWith
- Netcraft
- Whois
- grep.app
- Google dorking

---

# In-Scope Assets

## Primary Targets

- api-*.netflix.com
- api.netflix.com
- *.prod.ftl.netflix.com
- *.prod.cloud.netflix.com
- *.prod.dradis.netflix.com
- www.netflix.com
- secure.netflix.com
- ichnaea.netflix.com
- beacon.netflix.com
- *.nflxvideo.net
- *.nflxext.com
- *.nflximg.net
- *.nflxso.net
- help.netflix.com
- meechum.netflix.com

## Beacon Aliases

- customerevents.netflix.com
- nmtracking.netflix.com
- presentationtracking.netflix.com

---

# Prioritised Potential Entry Points

| Rank | Asset | Source | Why It Matters |
|------|-------|--------|----------------|
|1|api.netflix.com|HackerOne|Core API infrastructure and authentication workflows.|
|2|www.netflix.com|HackerOne|Primary user-facing application.|
|3|secure.netflix.com|HackerOne|Security-sensitive asset delivery.|
|4|meechum.netflix.com|HackerOne|Partner integrations and possible SSO exposure.|
|5|help.netflix.com|HackerOne|Support workflows and phishing research.|
|6|beacon.netflix.com|HackerOne|Client telemetry collection.|
|7|ichnaea.netflix.com|HackerOne|Logging endpoint.|
|8|*.prod.cloud.netflix.com|HackerOne|Production infrastructure.|
|9|*.prod.ftl.netflix.com|HackerOne|Production service infrastructure.|
|10|*.prod.dradis.netflix.com|HackerOne|Production environment naming convention.|

---

# Evidence Collection

## crt.sh Findings

Certificates observed:

- 27062559317
- 25609354274
- 25485417042

Observed:

- Cloudflare usage
- sha256WithRSAEncryption

These findings are certificate metadata only.

---

## Censys Findings

Observed software:

- cloudflare
- apache
- amazon
- f5
- openresty
- cpanel
- php
- fastly
- dovecot
- roundcube
- exim
- express
- wordpress

Observed services:

- nginx
- s3
- cloudflare_load_balancer
- waf
- openssh
- webmail
- next.js
- elastic_load_balancing

**Validation note:**

These results must not automatically be attributed to Netflix infrastructure. Ownership verification against Netflix ASN/netblocks is required before treating them as Netflix assets.

The previous Dovecot vulnerability statement was removed.

---

## FOFA Findings

Observed:

Apache/2.4.52 (Ubuntu)

Validation required before attribution.

---

## Whois Findings

Observed:

### A Records

- 3.225.92.8
- 54.160.93.182
- 3.211.157.115

### MX Records

Google mail infrastructure.

### Nameservers

AWS DNS.

### CNAME

www.netflix.com -> www.prod.ftl.netflix.com

---

## BuiltWith Findings

Observed subdomains:

- jobs.netflix.com
- techblog.netflix.com
- account.netflix.com
- partner.netflix.com
- research.netflix.com
- api-public.netflix.com
- contenthub.netflix.com

JavaScript observations:

- 9 external JavaScript files loaded.

Validation required because BuiltWith contains historical assets.

---

## grep.app Findings

Observed references to:

- api.netflix.com
- nflximg.com
- catalog endpoints

Useful for naming conventions.

---

## Netcraft Findings

Observed:

- Hosting company: Amazon
- ASN: AS40027
- Reverse DNS: prod.ftl4.netflix.com
- Registrar: MarkMonitor
- DNSSEC: Enabled

These findings provide stronger ownership evidence.

---

# Threat Actor Framing

## Credential Stuffing and Account Resale Groups

Targets:

- www.netflix.com
- help.netflix.com

## Social Engineering Actors

Targets:

- help.netflix.com
- secure.netflix.com
- meechum.netflix.com

## Infrastructure Intelligence Actors

Targets:

- api.netflix.com
- beacon.netflix.com
- ichnaea.netflix.com

---

# Limitations

- Passive OSINT only.
- Tool output is not proof of ownership.
- Historical results require validation.
- No vulnerabilities were tested.
- No active interaction occurred.
