# Netcat Port Scanning and Banner Grabbing

- Netcat (`nc`) is a raw TCP/UDP connection tool.
- Many services announce themselves immediately on connection (SSH, FTP, SMTP) — this alone can confirm software and version without a full scan.
- Example
    
    ```bash
    ┌──(elnem㉿kali)-[~]
    └─$ nc -nv 45.33.32.156 22
    Connection to 45.33.32.156 22 port [tcp/*] succeeded!
    SSH-2.0-OpenSSH_6.6.1p1 Ubuntu-2ubuntu2.13
    ```
    
- Netcat Cheat Sheet:

---

# TCP/UDP Port Scanning

#### TCP Connect Scanning

- Completes the full TCP three-way handshake (SYN → SYN-ACK → ACK) with the target.
- Reliable, but noisy — every connection attempt is logged by the target, since it's a fully established connection.

#### Stealth / SYN Scanning

- Sends a SYN packet and waits for SYN-ACK, then immediately sends a RST instead of completing the handshake with ACK.
- Faster and quieter than a full connect scan, since the connection is never fully established (some older logging systems won't record it as a full connection). Requires raw socket privileges (root/administrator).

#### UDP Scanning Mechanics and Limitations

- UDP has no handshake — a scanner sends a UDP packet and waits. If the port is closed, the target typically responds with an ICMP "port unreachable" message.
- If open, there may be **no response at all** (many UDP services only reply to correctly formatted application-layer requests), which is why UDP scanning is slow and prone to false "open|filtered" results.
- This is also why UDP scans take dramatically longer than TCP scans.

---

# **Host Discovery / Network Sweeping**

- Before scanning ports at all, you often want to know which hosts in a range are even alive:

```bash
nmap -sn 10.10.10.0/24        # ping sweep, no port scan
fping -a -g 10.10.10.0/24     # fast alternative sweep tool
```

---

# **OS Fingerprinting Basics**

- Nmap can guess a target's OS by analyzing subtle differences in how its TCP/IP stack responds (TTL values, window sizes, TCP option ordering):
    
    ```bash
    nmap -O 10.10.10.5
    ```
    

---

# Port Scanning with Nmap

**Basic scan (top 1000 ports):**

```bash
nmap 10.10.10.5
```

**Full port range:**

```bash
nmap -p- 10.10.10.5
```

**Targeted scan (specific ports):**

```bash
nmap -p 22,80,445,3389 10.10.10.5
```

**Version Detection (-sV):**

```bash
nmap -sV 10.10.10.5
```

**Default and Custom NSE Script Scanning:**

```bash
nmap -sC 10.10.10.5                        # default safe scripts
nmap --script=smb-vuln* 10.10.10.5         # custom script category
nmap --script vuln 10.10.10.5              # vulnerability-focused scripts
```

- NSE (Nmap Scripting Engine) scripts range from safe enumeration to active vulnerability checks — worth knowing the difference between script categories (`safe`, `intrusive`, `vuln`, `auth`, etc.) since some can crash fragile services.

**Aggressive Scanning (-A):**

```bash
nmap -A 10.10.10.5
```

**A practical full scan most people run first:**

```bash
nmap -sC -sV -p- -oN full_scan.txt 10.10.10.5
```

**Output Options and Result Organization:**

```bash
nmap -oN scan.txt 10.10.10.5      # normal readable output
nmap -oX scan.xml 10.10.10.5      # XML (parseable by other tools)
nmap -oG scan.grep 10.10.10.5     # grepable format
nmap -oA scan_all 10.10.10.5      # all three formats at once
```

---

# DNS Enumeration

#### Resource Record Types

| Record | Meaning |
| --- | --- |
| A | IPv4 address |
| AAAA | IPv6 address |
| MX | Mail server |
| NS | Nameserver |
| TXT | Arbitrary text (SPF, verification, sometimes leaks info) |
| CNAME | Alias to another hostname |
| SOA | Zone authority info |
| PTR | Reverse lookup record |

#### Forward and Reverse Lookups

```bash
dig target.com A                    # forward lookup
dig -x 10.10.10.5                   # reverse lookup
```

#### Zone Transfers

- A zone transfer (AXFR) is meant only for authorized secondary DNS servers to sync zone data — but a misconfigured DNS server will hand the **entire zone file** (every record it holds) to anyone who asks:
    
    ```bash
    dig axfr @ns1.target.com target.com
    ```
    
- If successful, this can reveal every subdomain, internal hostname, and mail server in one request — a huge misconfiguration when it works.

#### Subdomain Brute-Forcing

```bash
gobuster dns -d target.com -w /usr/share/wordlists/subdomains.txt
```

- Or with `dnsenum`, `dnsrecon`, `fierce` — all automate the same core idea: trying common subdomain names against the target's DNS.

#### Automated Tools and Windows-Native Options

```
nslookup target.com                 # Windows/cross-platform basic lookup
nslookup -type=MX target.com        # specific record type on Windows
```

---

# SMB Enumeration

#### smbclient

```bash
smbclient -L //10.10.10.5 -N        # list shares, -N = no password (null session)
smbclient //10.10.10.5/SHARENAME -N # connect to a specific share
```

#### smbmap

```bash
smbmap -H 10.10.10.5
smbmap -H 10.10.10.5 -u null -p ''  # explicit null session
```

- Shows share names and your access level (Read/Write/No Access) per share in one clean output — often faster to scan than smbclient for an overview.

#### enum4linux

```bash
enum4linux -a 10.10.10.5
```

- `a` runs all enumeration modules: OS info, users, groups, shares, password policy — a strong first pass against any SMB target.

#### rpcclient / NetBIOS Techniques

```bash
rpcclient -U "" -N 10.10.10.5
# then inside the rpcclient prompt:
srvinfo
enumdomusers
querydominfo
```

```bash
nbtstat -A 10.10.10.5               # NetBIOS name enumeration (Windows-native)
nmblookup -A 10.10.10.5             # Linux equivalent
```

#### Nmap SMB Scripts

```bash
nmap --script smb-os-discovery,smb-enum-shares,smb-enum-users -p 445 10.10.10.5
```

---

# SMTP Enumeration

#### VRFY / EXPN Commands

- Legacy SMTP commands intended for mail administrators, but often left enabled — can be abused to confirm valid usernames:
    
    ```bash
    nc -nv 10.10.10.5 25
    VRFY root
    VRFY nonexistentuser
    ```
    
- A different response (accepted vs. rejected) between a real and fake username confirms user enumeration is possible.

#### Banner Grabbing and User Enumeration

```bash
nc -nv 10.10.10.5 25
```

- The banner on connect often reveals the exact mail server software and version (Postfix, Exim, Sendmail, Exchange).

#### Nmap SMTP Scripts

```bash
nmap --script smtp-enum-users -p 25 10.10.10.5
nmap --script smtp-commands -p 25 10.10.10.5
```

---

# SNMP Enumeration

- SNMP (Simple Network Management Protocol) is often overlooked but can leak enormous amounts of internal information when misconfigured with default/weak community strings.

#### snmpwalk

```bash
snmpwalk -c public -v1 10.10.10.5
```

- Walks the entire accessible MIB tree, dumping every value the community string has access to.

#### Community Strings

- `public` — typically read-only, the most common default
- `private` — typically read-write, far more dangerous if left default, since it can allow configuration changes
Always test both as a first step — SNMP misconfigurations with default strings are still common in the wild and are a classic OSCP-lab-style finding.

#### MIB Tree Probing and Useful OIDs

| OID | Reveals |
| --- | --- |
| 1.3.6.1.2.1.1.1.0 | System description |
| 1.3.6.1.2.1.25.1.6.0 | System processes |
| 1.3.6.1.4.1.77.1.2.25 | Windows user accounts (on some systems) |
| 1.3.6.1.2.1.6.13.1.3 | TCP listening ports |

```bash
snmpwalk -c public -v1 10.10.10.5 1.3.6.1.2.1.25.4.2.1.2   # running processes
```

#### Related Tools and Nmap Scripts

```bash
nmap -sU --script snmp-processes,snmp-netstat,snmp-win32-users -p 161 10.10.10.5
onesixtyone -c community_strings.txt 10.10.10.5   # fast community string brute-forcer
```
