# SMTP Enumeration

Platform: General
Status: Solid
Tags: Enumeration
Type: cheat sheet

# Manual Banner Grabbing & Interaction

```bash
# Netcat (recommended)
nc -nv <IP> 25
nc -C <IP> 25          # better line ending handling

# Telnet
telnet <IP> 25
```

#### **Useful commands once connected**:

```
HELO test
EHLO test
VRFY root
VRFY admin
EXPN root
EXPN postmaster
MAIL FROM: test@test.com
RCPT TO: admin@target.com
RCPT TO: root
QUIT
```

---

# User Enumeration Methods

| Method | Command | Description | Notes |
| --- | --- | --- | --- |
| **VRFY** | `VRFY username` | Asks server if user exists | Most common, often disabled |
| **EXPN** | `EXPN username` | Expands mailing lists / aliases | Frequently disabled |
| **RCPT TO** | `RCPT TO: user@domain` | Checks if recipient is accepted | Most reliable when VRFY/EXPN are off |

---

# smtp-user-enum

```bash
# VRFY method
smtp-user-enum -M VRFY -U users.txt -t <IP>
smtp-user-enum -M VRFY -u root -t <IP>

# EXPN method
smtp-user-enum -M EXPN -U users.txt -t <IP>

# RCPT TO method (usually most effective)
smtp-user-enum -M RCPT -U users.txt -t <IP>
smtp-user-enum -M RCPT -U users.txt -t <IP> -D target.com

# Common wordlists
smtp-user-enum -M VRFY -U /usr/share/seclists/Usernames/top-usernames-shortlist.txt -t <IP>
smtp-user-enum -M RCPT -U /usr/share/seclists/Usernames/Names/names.txt -t <IP>
```

---

# Nmap smtp-enum-users Script

```bash
# Default
nmap -p 25 --script smtp-enum-users <IP>

# Specify methods and wordlist
nmap -p 25 --script smtp-enum-users \
  --script-args smtp-enum-users.methods={VRFY,EXPN,RCPT},userdb=/usr/share/seclists/Usernames/top-usernames-shortlist.txt <IP>
```

```bash
nmap -p 25 --script smtp-commands <IP>          # Shows supported commands
nmap -p 25 --script smtp-open-relay <IP>        # Check if open relay
nmap -p 25 --script smtp-ntlm-info <IP>         # NTLM info disclosure
nmap -p 25 --script smtp-vuln-cve2011-1764 <IP> # Specific vulnerability
```

---

# Quick Manual Loop

```
for user in root admin administrator test guest info postmaster;do
  echo -e "VRFY$user\nQUIT" | nc -nv -w 2 <IP> 25
done
```