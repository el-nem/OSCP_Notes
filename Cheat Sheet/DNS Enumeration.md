# DNS Enumeration

Status: Solid
Tags: Enumeration
Type: cheat sheet

## dig

```bash
dig target.com                      # default A record lookup
dig target.com A
dig target.com MX                   # mail servers
dig target.com TXT                  # TXT records (SPF, verification tokens)
dig target.com NS                   # nameservers
dig target.com ANY                  # all record types (many servers now refuse this)
dig -x 10.10.10.5                   # reverse lookup (PTR)
dig target.com @8.8.8.8             # query a specific resolver
dig +short target.com               # concise output, just the answer
```

### Zone Transfer with dig

```bash
dig axfr @ns1.target.com target.com
```

Only works against misconfigured DNS servers that allow unauthenticated zone transfers — but when it works, it dumps the entire DNS zone (every subdomain/host record) in one request.

## nslookup

```bash
nslookup target.com                     # basic lookup
nslookup -type=MX target.com            # specific record type
nslookup -type=NS target.com
nslookup target.com 8.8.8.8             # query specific server
```

Available natively on both Windows and Linux — the go-to when you have a limited shell with no extra tools installed.

### Interactive mode (useful on Windows, no other tools available)

```
nslookup
> server 10.10.10.5
> set type=ANY
> target.com
```

## Subdomain Brute-Forcing

### Gobuster (DNS mode)

```bash
gobuster dns -d target.com -w /usr/share/wordlists/subdomains-top1million-5000.txt
gobuster dns -d target.com -w wordlist.txt -t 50    # 50 threads
gobuster dns -d target.com -w wordlist.txt -i       # show IPs in output
```

### dnsenum

```bash
dnsenum target.com
dnsenum --dnsserver 10.10.10.5 target.com
dnsenum -f subdomains.txt target.com    # custom wordlist brute force
```

### dnsrecon

```bash
dnsrecon -d target.com                      # standard enumeration
dnsrecon -d target.com -t axfr              # zone transfer attempt only
dnsrecon -d target.com -D wordlist.txt -t brt   # brute force with specific wordlist
```

### fierce

```bash
fierce --domain target.com
fierce --domain target.com --subdomain-file wordlist.txt
```