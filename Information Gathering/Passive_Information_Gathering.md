# Main Approaches to Passive Information Gathering

- **Open Source Intelligence (OSINT) / Public Sources** ⇒ Gathering data from sources that are already public (company websites, social media, forums, public code repositories, news articles, job postings
- **Third-party Aggregators / Historical Data** ⇒ Using third-party infrastructure that has *already* interacted with or scanned the target, so you never touch it yourself (WHOIS registries, DNS registrars, certificate transparency logs, and pre-built internet scanning databases like Shodan/Censys/Netcraft)

---

# WHOIS

- `WHOIS` is a query/response protocol defined in RFC 3912. WHOIS servers listen on **TCP port 43** and provide registration details for domain names.
- From `WHOIS`, we extract :
    - Registrant / organization name
    - Email addresses & phone numbers (often redacted now)
    - Name servers (NS)
    - Registrar
    - Creation/expiration/update dates
    - IP ranges sometimes linked
- Example
    - command
    
    ```bash
    whois example.com
    whois example.com -h whois.verisign-grs.com   # specific server
    ```
    
    - Output
    
    ```bash
       Domain Name: EXAMPLE.COM
       Registry Domain ID: 2336799_DOMAIN_COM-VRSN
       Registrar WHOIS Server: whois.iana.org
       Registrar URL: http://res-dom.iana.org
       Updated Date: 2026-01-16T18:26:50Z
       Creation Date: 1995-08-14T04:00:00Z
       Registry Expiry Date: 2026-08-13T04:00:00Z
       Registrar: RESERVED-Internet Assigned Numbers Authority
       Registrar IANA ID: 376
       Registrar Abuse Contact Email:
       Registrar Abuse Contact Phone:
       Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
       Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
       Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
       Name Server: ELLIOTT.NS.CLOUDFLARE.COM
       Name Server: HERA.NS.CLOUDFLARE.COM
       DNSSEC: signedDelegation
       DNSSEC DS Data: 2371 13 2 C988EC423E3880EB8DD8A46FE06CA230EE23F35B578D64E78B29C3E1C83D245A
       URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
    >>> Last update of whois database: 2026-08-04T21:42:55Z <<<
    
    For more information on Whois status codes, please visit https://icann.org/epp
    
    NOTICE: The expiration date displayed in this record is the date the
    registrar's sponsorship of the domain name registration in the registry is
    currently set to expire. This date does not necessarily reflect the expiration
    date of the domain name registrant's agreement with the sponsoring
    registrar.  Users may consult the sponsoring registrar's Whois database to
    view the registrar's reported date of expiration for this registration.
    
    TERMS OF USE: You are not authorized to access or query our Whois
    database through the use of electronic processes that are high-volume and
    automated except as reasonably necessary to register domain names or
    modify existing registrations; the Data in VeriSign Global Registry
    Services' ("VeriSign") Whois database is provided by VeriSign for
    information purposes only, and to assist persons in obtaining information
    about or related to a domain name registration record. VeriSign does not
    guarantee its accuracy. By submitting a Whois query, you agree to abide
    by the following terms of use: You agree that you may use this Data only
    for lawful purposes and that under no circumstances will you use this Data
    to: (1) allow, enable, or otherwise support the transmission of mass
    unsolicited, commercial advertising or solicitations via e-mail, telephone,
    or facsimile; or (2) enable high volume, automated, electronic processes
    that apply to VeriSign (or its computer systems). The compilation,
    repackaging, dissemination or other use of this Data is expressly
    prohibited without the prior written consent of VeriSign. You agree not to
    use electronic processes that are automated and high-volume to access or
    query the Whois database except as reasonably necessary to register
    domain names or modify existing registrations. VeriSign reserves the right
    to restrict your access to the Whois database in its sole discretion to ensure
    operational stability.  VeriSign may restrict or terminate your access to the
    Whois database for failure to abide by these terms of use. VeriSign
    reserves the right to modify these terms at any time.
    
    The Registry database contains ONLY .COM, .NET, .EDU domains and
    Registrars.
    % IANA WHOIS server
    % for more information on IANA, visit http://www.iana.org
    % This query returned 1 object
    
    domain:       EXAMPLE.COM
    
    organisation: Internet Assigned Numbers Authority
    
    created:      1992-01-01
    source:       IANA
    
    ```
    
- Sites:whois.com, whois.icann.org.

---

# DNS Passive Information Gathering

- DNS passive information gathering: collects domain configuration and historical records through third-party databases and cached logs without sending direct queries to a target's authoritative name servers.
- **Common record types**:
    - A / AAAA → IP addresses
    - NS → Name servers
    - MX → Mail servers
    - TXT → SPF, DKIM, verification strings, sometimes secrets
    - CNAME → Aliases
    - SOA → Start of Authority
- Example
    - command
    
    ```bash
    dig example.com ANY
    dig example.com MX
    dig example.com NS
    dig example.com TXT
    host example.com
    nslookup example.com
    ```
    
    - Output
    
    ```bash
    dig example.com ANY
    
    ; <<>> DiG 9.20.23-1-Debian <<>> example.com ANY
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23325
    ;; flags: qr rd ra ad; QUERY: 1, ANSWER: 21, AUTHORITY: 0, ADDITIONAL: 11
    
    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 512
    ;; QUESTION SECTION:
    ;example.com.                   IN      ANY
    
    ;; ANSWER SECTION:
    example.com.            266     IN      TXT     "_k2n1y4vw3qtb4skdx9e7dxt97qrmmq9"
    example.com.            266     IN      TXT     "v=spf1 -all"
    example.com.            266     IN      RRSIG   TXT 13 2 300 20260805225240 20260803205240 34505 example.com. XXuv9vz+O3dgiOEeslYfA5wUPkI2WMbdqu1xX5NS3I0Z2xSk/d6KVdDK SKUqmhfnG72tq+Kh5RbRtdCrdwWKPQ==
    example.com.            2586    IN      DNSKEY  256 3 13 MjyZielP0GqniI1+j+wAG/3t0ImDDIlj1CxR0oobkZQHSKH2Fqx6tm2N cYu57POJ83SzCWLkqIjZHS1mh5wbaw==
    example.com.            2586    IN      DNSKEY  257 3 13 mdsswUyr3DPW132mOi8V9xESWE8jTo0dxCjjnopKl+GqJxpVXckHAeF+ KkxLbxILfDLUT0rAK9iUzy1L53eKGQ==
    example.com.            2586    IN      DNSKEY  256 3 13 oJMRESz5E4gYzS/q6XDrvU1qMPYIjCWzJaOau8XNEZeqCYKD5ar0IRd8 KqXXFJkqmVfRvMGPmM1x8fGAa2XhSA==
    example.com.            2586    IN      DNSKEY  256 3 13 kxipjoIbNZDsWqEKaYaGq6fM/XThrRp1ue6AV9R/n3eWxpGCeCWJb47P EEEj/Q6VAYFW/7UFo5mXoZfxKYZa3A==
    example.com.            2586    IN      RRSIG   DNSKEY 13 2 3600 20260914174644 20260715174644 2371 example.com. /uOliJCR+LGrNNgrYH4Ei49ABDXdmDSY5JEGkvK1WT5xVHPhOCXNBu1q g0CCbLNF80202cXTWMDhCwSTZDUP5w==
    example.com.            198     IN      AAAA    2606:4700:10::6814:179a
    example.com.            198     IN      AAAA    2606:4700:10::ac42:93f3
    example.com.            198     IN      RRSIG   AAAA 13 2 300 20260805225132 20260803205132 34505 example.com. au+fsjpqAMAwG+xqz7RrqjHntArI9miH0cnxORYLpju0+LwGepge6W0c yD+DBK3eFyWZOsEsRJKhVOHw4LPEgw==
    example.com.            86361   IN      NS      hera.ns.cloudflare.com.
    example.com.            86361   IN      NS      elliott.ns.cloudflare.com.
    example.com.            86361   IN      RRSIG   NS 13 2 86400 20260805225235 20260803205235 34505 example.com. yJNVbv4+N/g1xyMFMJT3FOJ9ff2ZGy5L2dLjkLb8FL06J5xM8Q1a+Upq jv6OJiLh21CZXzLbnwE8d3fBd0V8Ig==
    example.com.            135     IN      A       104.20.23.154
    example.com.            135     IN      A       172.66.147.243
    example.com.            135     IN      RRSIG   A 13 2 300 20260805225029 20260803205029 34505 example.com. 67gh1i8jVCQBmxaZtntH+fv32tfD+OVpoZrrG3BFuk/xquBk8A5/Skxf eqNmjNo8C8HHZCgteWye7FxN9/3UXQ==
    example.com.            227     IN      HTTPS   1 . alpn="h2" ipv4hint=104.20.23.154,172.66.147.243 ipv6hint=2606:4700:10::6814:179a,2606:4700:10::ac42:93f3
    example.com.            227     IN      RRSIG   HTTPS 13 2 300 20260805225201 20260803205201 34505 example.com. 7lt8ba2lP7CoQSdE+TFjIePi+dKkdruM+hZKgw4uligBqvmGpsRAPMpa KwH+oVuZgsvwng7ZxyQJ2vY05Kdx0w==
    example.com.            261     IN      MX      0 .
    example.com.            261     IN      RRSIG   MX 13 2 300 20260805225235 20260803205235 34505 example.com. mslFj2F0o/x3TwTcv+Qm3KXZnapM9ip+tjfQsScslAXudjvLG/lGdOsm hhzQSuL3L2Tf3xxjGRCZAn7vYIvb2A==
    
    ;; ADDITIONAL SECTION:
    elliott.ns.cloudflare.com. 17202 IN     A       108.162.195.228
    elliott.ns.cloudflare.com. 17202 IN     A       162.159.44.228
    elliott.ns.cloudflare.com. 17202 IN     A       172.64.35.228
    hera.ns.cloudflare.com. 85284   IN      A       172.64.32.162
    hera.ns.cloudflare.com. 85284   IN      A       173.245.58.162
    hera.ns.cloudflare.com. 85284   IN      A       108.162.192.162
    example.com.            135     IN      A       172.66.147.243
    example.com.            135     IN      A       104.20.23.154
    example.com.            198     IN      AAAA    2606:4700:10::6814:179a
    example.com.            198     IN      AAAA    2606:4700:10::ac42:93f3
    
    ;; Query time: 15 msec
    ;; SERVER: 192.168.214.2#53(192.168.214.2) (TCP)
    ;; WHEN: Tue Aug 04 17:53:14 EDT 2026
    ;; MSG SIZE  rcvd: 1590
    
    ```
    
- **tools**:
    - crt.sh
    - DNSDumpster
    - SecurityTrails
    - ViewDNS.info
    - theHarvester: `theHarvester -d example.com -b all`

---

# Open Source Intelligence (OSINT)

- Collecting and analyzing publicly available information:
    - **Company websites** — "About Us" pages, press releases, and careers pages often leak organizational structure and technology choices
    - **Job postings** — "5+ years Django experience, AWS, PostgreSQL" tells you the tech stack before you scan anything
    - **Social media (LinkedIn especially)** — employee names, roles, org structure — useful for understanding target scope and (in authorized engagements) building phishing pretexts or password-spray username lists
    - **Public forums / Stack Overflow** — developers sometimes post real (sanitized-looking but not actually sanitized) config snippets when asking for help debugging
    - **News articles and press releases** — mergers, acquisitions, and new offices often reveal newly added infrastructure or business relationships in scope
    - **Public breach data / paste sites** — previously leaked credentials tied to the organization's email domain (only reference for defensive/authorized use — never use as an excuse to access accounts you don't own)
- **Useful frameworks**:
    - OSINT Framework — Interactive map of tools
    - Recon-ng (modular framework, pre-installed on Kali)
    - SpiderFoot (open-source automated OSINT)
    - theHarvester (emails, subdomains, hosts)

---

# Google Hacking / Google Dorking

- Using advanced search operators to find information Google has already indexed that the target didn't intend to expose.
- **Essential operators**:
    - `site:example.com`
    - `filetype:pdf / filetype:xls / filetype:sql / filetype:env`
    - `intitle:"index of"`
    - `inurl:admin / inurl:login / inurl:backup`
    - `ext:log / ext:bak / ext:old`
    - `"password" filetype:txt site:example.com`
    - `"confidential" OR "internal use only" site:example.com`
- **Resources**:
    - Google Hacking Database (GHDB) on Exploit-DB
    - DorkSearch.com

---

# Netcraft

- Excellent for web technology and historical data.
- **Sites**:
    - sitereport.netcraft.com — Site report (server, OS, history)
    - searchdns.netcraft.com — DNS search & related sites
- **What it reveals:**
    - Web server software and version (Apache/Nginx/IIS)
    - Hosting provider and history of hosting changes over time
    - Site technology (CMS, frameworks) via its "Site Report"
    - SSL certificate details and history

---

# **Open-Source Code / GitHub Secret Discovery**

- Developers accidentally commit secrets to public repositories constantly — API keys, database credentials, internal hostnames, even full config files.
- **Manual search approach:**
    - `site:github.com "target.com" api_key`
    - `site:github.com "target.com" password`
- **What to look for:**
    - `.env` files accidentally committed
    - Hardcoded API keys/tokens in config files
    - Internal hostnames or IP ranges referenced in code comments
    - CI/CD configuration files (`.gitlab-ci.yml`, GitHub Actions workflows) that sometimes reference internal infrastructure
- Tools:
    - trufflehog
    - gitleaks

---

# Shodan

- Shodan (shodan.io) is a search engine that continuously scans the entire internet and indexes the results(Search engine for internet-connected devices).
- **Core searches:**
    - `hostname:target.com`
    - `org:"Target Organization Name"`
    - `ssl:"target.com"`
- **What it reveals:**
    - Open ports and the banners/service versions running on them
    - Exposed IoT devices, cameras, industrial control systems (if any belong to the target)
    - Historical scan data — what was running on a host previously
    - Geographic location of infrastructure

---

# Web Server Passive Information Gathering

- **Wayback Machine** (web.archive.org) — historical snapshots of the site, sometimes revealing old pages, endpoints, or comments removed from the current live version
- **BuiltWith** (builtwith.com) — technology profiling similar to Netcraft, focused on marketing/analytics/CMS stack detection
- **Robots.txt and sitemap.xml** — viewing these via a normal browser request reveals disallowed paths (which often hint at admin panels or sensitive sections) and a full site structure map
- **HTTP response via a simple browser visit** — server header, cookies set, redirect behavior — all observable without any scanning tool

---

# SSL/TLS Hardening & Certificate Checks

- **What to examine**:
    - Certificate validity & chain
    - Supported protocols (TLS 1.0/1.1 are weak)
    - Cipher suites (avoid weak ones)
    - Heartbleed, POODLE, BEAST, etc.
    - HSTS preload status
    - Certificate Transparency
- **Tools**:
    - ssllabs.com/ssltest (Qualys) — Industry standard, gives A–F grade
    - Hardenize
    - testssl.sh (command-line, very thorough)
    - `openssl s_client -connect example.com:443`
