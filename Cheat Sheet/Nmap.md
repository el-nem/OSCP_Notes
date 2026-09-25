# Start

| Switch | Example | Description |
|---|---|---|
| `-sn` | `nmap -sn 192.168.1.0/24` | Discover what's alive on your network |
| `-F` | `nmap -F 192.168.1.10` | Scan the most common 100 ports on a single target |
| `-sV -sC` | `nmap -sV -sC 192.168.1.10` | Runs service detection (`-sV`) and default scripts (`-sC`) to identify what's actually running on open ports |

# Target Specification

| Switch | Example | Description |
|---|---|---|
| | `nmap 192.168.1.1` | Scan a single IP |
| | `nmap 192.168.1.1 192.168.2.1` | Scan specific IPs |
| | `nmap 192.168.1.1-254` | Scan a range |
| | `nmap scanme.nmap.org` | Scan a domain |
| | `nmap 192.168.1.0/24` | Scan using CIDR notation |
| `-iL` | `nmap -iL targets.txt` | Scan targets from a file |
| `-iR` | `nmap -iR 100` | Scan 100 random hosts |
| `--exclude` | `nmap --exclude 192.168.1.1` | Exclude listed hosts |
| `-6` | `nmap -6 2001:db8::1` | Scan an IPv6 target |

# Host Discovery

| Switch | Example | Description |
|---|---|---|
| `-sL` | `nmap 192.168.1.1-3 -sL` | No scan. List targets only |
| `-sn` | `nmap 192.168.1.1/24 -sn` | Disable port scanning. Host discovery only |
| `-Pn` | `nmap 192.168.1.1-5 -Pn` | Disable host discovery. Port scan only |
| `-PS` | `nmap 192.168.1.1-5 -PS22-25,80` | TCP SYN discovery on port x. Port 80 by default |
| `-PA` | `nmap 192.168.1.1-5 -PA22-25,80` | TCP ACK discovery on port x. Port 80 by default |
| `-PU` | `nmap 192.168.1.1-5 -PU53` | UDP discovery on port x. Port 40125 by default |
| `-PR` | `nmap 192.168.1.1-1/24 -PR` | ARP discovery on local network |
| `-n` | `nmap 192.168.1.1 -n` | Never do DNS resolution |

# Nmap Scan Techniques

| Switch | Example | Description |
|---|---|---|
| `-sS` | `nmap 192.168.1.1 -sS` | TCP SYN port scan (default). Requires root, otherwise falls back to `-sT` |
| `-sT` | `nmap 192.168.1.1 -sT` | TCP connect port scan (default without root privilege) |
| `-sU` | `nmap 192.168.1.1 -sU` | UDP port scan |
| `-sA` | `nmap 192.168.1.1 -sA` | TCP ACK port scan |
| `-sW` | `nmap 192.168.1.1 -sW` | TCP Window port scan |
| `-sM` | `nmap 192.168.1.1 -sM` | TCP Maimon port scan |
| `-sY` | `nmap 192.168.1.1 -sY` | SCTP INIT scan |
| `-sZ` | `nmap 192.168.1.1 -sZ` | SCTP COOKIE-ECHO scan |

# Port Specification

| Switch | Example | Description |
|---|---|---|
| `-p` | `nmap 192.168.1.1 -p 21` | Port scan for port x |
| `-p` | `nmap 192.168.1.1 -p 21-100` | Port range |
| `-p` | `nmap 192.168.1.1 -p U:53,T:21-25,80` | Port scan multiple TCP and UDP ports |
| `-p-` | `nmap 192.168.1.1 -p-` | Port scan all 65535 ports |
| `-p` | `nmap 192.168.1.1 -p http,https` | Port scan from service name |
| `-F` | `nmap 192.168.1.1 -F` | Fast port scan (top 100 ports) |
| `--top-ports` | `nmap 192.168.1.1 --top-ports 2000` | Port scan the top x most common ports |
| `-p-65535` | `nmap 192.168.1.1 -p-65535` | Leaving off initial port in range makes the scan start at port 1 |
| `-p0-` | `nmap 192.168.1.1 -p0-` | Leaving off end port in range makes the scan go through to port 65535 |
| `-r` | `nmap 192.168.1.1 -r` | Scan ports sequentially instead of randomizing order |

# Service and Version Detection

| Switch | Example | Description |
|---|---|---|
| `-sV` | `nmap 192.168.1.1 -sV` | Attempts to determine the version of the service running on port |
| `-sV --version-intensity` | `nmap 192.168.1.1 -sV --version-intensity 8` | Intensity level 0 to 9. Higher number increases possibility of correctness |
| `-sV --version-light` | `nmap 192.168.1.1 -sV --version-light` | Enable light mode. Lower possibility of correctness. Faster |
| `-sV --version-all` | `nmap 192.168.1.1 -sV --version-all` | Enable intensity level 9. Higher possibility of correctness. Slower |
| `-A` | `nmap 192.168.1.1 -A` | Enables OS detection, version detection, script scanning, and traceroute |

# OS Detection

| Switch | Example | Description |
|---|---|---|
| `-O` | `nmap 192.168.1.1 -O` | Remote OS detection using TCP/IP stack fingerprinting |
| `-O --osscan-limit` | `nmap 192.168.1.1 -O --osscan-limit` | If at least one open and one closed TCP port are not found it will not try OS detection against host |
| `-O --osscan-guess` | `nmap 192.168.1.1 -O --osscan-guess` | Makes Nmap guess more aggressively |
| `-O --max-os-tries` | `nmap 192.168.1.1 -O --max-os-tries 1` | Set the maximum number x of OS detection tries against a target |
| `-A` | `nmap 192.168.1.1 -A` | Enables OS detection, version detection, script scanning, and traceroute |

# Timing, Performance and Rate Control

| Switch | Example | Description |
|---|---|---|
| `-T0` | `nmap 192.168.1.1 -T0` | Paranoid (0) Intrusion Detection System evasion |
| `-T1` | `nmap 192.168.1.1 -T1` | Sneaky (1) Intrusion Detection System evasion |
| `-T2` | `nmap 192.168.1.1 -T2` | Polite (2) slows down the scan to use less bandwidth and use less target machine resources |
| `-T3` | `nmap 192.168.1.1 -T3` | Normal (3) which is default speed |
| `-T4` | `nmap 192.168.1.1 -T4` | Aggressive (4) speeds scans; assumes you are on a reasonably fast and reliable network |
| `-T5` | `nmap 192.168.1.1 -T5` | Insane (5) speeds scan; assumes you are on an extraordinarily fast network |
| `--min-rate` | `nmap 192.168.1.1 -p- --min-rate 5000` | Send packets no slower than x per second. The main lever for speeding up large scans |
| `--max-rate` | `nmap 192.168.1.1 --max-rate 100` | Send packets no faster than x per second |
| `--min-parallelism` | `nmap 192.168.1.1 --min-parallelism 100` | Minimum number of probes to run in parallel |
| `--max-retries` | `nmap 192.168.1.1 --max-retries 1` | Cap retransmissions of probes, speeds up scans on reliable networks |
| `--host-timeout` | `nmap 192.168.1.1 --host-timeout 5m` | Give up on a slow or unresponsive host after x time |

Note: `-T4` alone often isn't enough on a full `-p-` sweep against a large range. Pairing it with `--min-rate 5000` cuts scan time significantly: `nmap -p- --min-rate 5000 -T4 <target>`, then run a focused `-sV -sC` against whatever ports come back.

# NSE Scripts

| Switch | Example | Description |
|---|---|---|
| `-sC` | `nmap 192.168.1.1 -sC` | Scan with default NSE scripts. Considered useful for discovery and safe |
| `--script default` | `nmap 192.168.1.1 --script default` | Scan with default NSE scripts. Considered useful for discovery and safe |
| `--script` | `nmap 192.168.1.1 --script=banner` | Scan with a single script. Example banner |
| `--script` | `nmap 192.168.1.1 --script=http*` | Scan with a wildcard. Example http |
| `--script` | `nmap 192.168.1.1 --script=http,banner` | Scan with two scripts. Example http and banner |
| `--script` | `nmap 192.168.1.1 --script "not intrusive"` | Scan default, but remove intrusive scripts |
| `--script-args` | `nmap --script snmp-sysdescr --script-args snmpcommunity=admin 192.168.1.1` | NSE script with arguments |

### NSE Script Categories

| Category | Description |
|---|---|
| `auth` | Deals with authentication bypass or credential access |
| `safe` | Not intrusive, unlikely to crash the target or trigger alerts |
| `intrusive` | Could crash a service, use significant resources, or be considered aggressive |
| `vuln` | Checks for specific known vulnerabilities |
| `exploit` | Actively attempts to exploit a vulnerability |
| `brute` | Runs brute-force password auditing |
| `discovery` | Tries to learn more about the network (service enumeration, etc.) |
| `default` | Scripts run automatically with `-sC`, a mix of safe and discovery |

Run a whole category with `--script <category>`, e.g. `nmap --script vuln 192.168.1.1`. Categories can be combined: `--script "vuln and safe"`.

### Useful NSE Script Examples

| Command | Description |
|---|---|
| `nmap -Pn --script=http-sitemap-generator scanme.nmap.org` | http site map generator |
| `nmap -n -Pn -p 80 --open -sV -vvv --script banner,http-title -iR 1000` | Fast search for random web servers |
| `nmap -Pn --script=dns-brute domain.com` | Brute forces DNS hostnames guessing subdomains |
| `nmap -n -Pn -vv -O -sV --script smb-enum*,smb-ls,smb-mbenum,smb-os-discovery,smb-s*,smb-vuln*,smbv2* 192.168.1.1` | Safe SMB scripts to run |
| `nmap --script whois* domain.com` | Whois query |
| `nmap -p80 --script http-unsafe-output-escaping scanme.nmap.org` | Detect cross site scripting vulnerabilities |
| `nmap -p80 --script http-sql-injection scanme.nmap.org` | Check for SQL injections |

# UDP Scanning

UDP scans are slow because closed ports often don't respond, forcing Nmap to wait out a timeout on every probe. Avoid running `-sU -p- --min-rate 5000` blindly on a whole range, narrow down first.

| Switch | Example | Description |
|---|---|---|
| `-sU` | `nmap -sU --top-ports 20 192.168.1.1` | Scan only the top 20 UDP ports first for a quick triage |
| `-sU -sV` | `nmap -sU -sV -p 53,67,68,69,123,161,162,500 192.168.1.1` | Version-scan the common UDP services: DNS, DHCP, TFTP, NTP, SNMP, IKE |
| `--defeat-icmp-ratelimit` | `nmap -sU --defeat-icmp-ratelimit 192.168.1.1` | Works around a target's ICMP rate limiting that slows UDP scans down |

A reasonable workflow: quick `--top-ports 20` UDP scan for triage, then a targeted `-sV -sC` against whatever's open, and a full `-p-` UDP sweep only if there's time to spare since it can take hours.

# Firewall / IDS Evasion and Spoofing

| Switch | Example | Description |
|---|---|---|
| `-f` | `nmap 192.168.1.1 -f` | Requested scan (including ping scans) use tiny fragmented IP packets. Harder for packet filters |
| `--mtu` | `nmap 192.168.1.1 --mtu 32` | Set your own offset size |
| `-D` | `nmap -D 192.168.1.101,192.168.1.102,192.168.1.103,192.168.1.23 192.168.1.1` | Send scans from spoofed IPs |
| `-D` | `nmap -D decoy-ip1,decoy-ip2,your-own-ip,decoy-ip3,decoy-ip4 remote-host-ip` | Above example explained |
| `-S` | `nmap -S www.microsoft.com www.facebook.com` | Scan Facebook from Microsoft (`-e eth0 -Pn` may be required) |
| `-g` | `nmap -g 53 192.168.1.1` | Use given source port number |
| `--proxies` | `nmap --proxies http://192.168.1.1:8080,http://192.168.1.2:8080 192.168.1.1` | Relay connections through HTTP/SOCKS4 proxies |
| `--data-length` | `nmap --data-length 200 192.168.1.1` | Appends random data to sent packets |

# Output

| Switch | Example | Description |
|---|---|---|
| `-oN` | `nmap 192.168.1.1 -oN normal.file` | Normal output to the file normal.file |
| `-oX` | `nmap 192.168.1.1 -oX xml.file` | XML output to the file xml.file |
| `-oG` | `nmap 192.168.1.1 -oG grep.file` | Grepable output to the file grep.file |
| `-oA` | `nmap 192.168.1.1 -oA results` | Output in the three major formats at once |
| `-oG -` | `nmap 192.168.1.1 -oG -` | Grepable output to screen. `-oN -`, `-oX -` also usable |
| `--append-output` | `nmap 192.168.1.1 -oN file.file --append-output` | Append a scan to a previous scan file |
| `-v` | `nmap 192.168.1.1 -v` | Increase the verbosity level (use `-vv` or more for greater effect) |
| `-d` | `nmap 192.168.1.1 -d` | Increase debugging level (use `-dd` or more for greater effect) |
| `--reason` | `nmap 192.168.1.1 --reason` | Display the reason a port is in a particular state, same output as `-vv` |
| `--open` | `nmap 192.168.1.1 --open` | Only show open (or possibly open) ports |
| `--packet-trace` | `nmap 192.168.1.1 -T4 --packet-trace` | Show all packets sent and received |
| `--iflist` | `nmap --iflist` | Shows the host interfaces and routes |
| `--resume` | `nmap --resume results.file` | Resume a scan |

# Port States

| State | Meaning |
|---|---|
| Open | A service is actively accepting connections on this port. This is your target, something is listening. |
| Closed | The port is accessible (no firewall blocking), but no service is listening. |
| Filtered | Nmap can't determine if the port is open because packet filtering (firewall, IPS, router ACL) is preventing probes from reaching it. You're not getting responses, you're getting silence. |
| Unfiltered | The port is accessible, but Nmap can't determine if it's open or closed. |
| Open\|Filtered | Nmap can't tell if the port is open or filtered. |
| Closed\|Filtered | Rare state, usually seen with IP ID idle scans. The port is either closed or filtered. |

# Troubleshooting

- Full `-p-` scan taking forever: add `--min-rate 5000 -T4`, and consider scanning TCP and UDP separately instead of together.
- Everything shows filtered: likely a firewall dropping probes. Try `-Pn` to skip host discovery, or switch scan type since `-sA` can reveal firewall rules a normal SYN scan can't.
- No root privileges available: `-sS`, `-O`, and some other scans silently degrade or fail, falling back to `-sT`. Check terminal output for warnings.
- Results differ between runs: rate limiting, IDS/IPS interference, or unstable network conditions can cause inconsistent results. Rerun with a lower `-T` and higher `--max-retries` to confirm.
