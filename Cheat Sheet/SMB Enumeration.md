# SMB Enumeration

Platform: General
Status: Solid
Tags: Enumeration
Type: cheat sheet

# smbclient

```bash
# List shares (null session)
smbclient -L //<IP> -N
smbclient -L //<IP> -U ""

# List shares with credentials
smbclient -L //<IP> -U "user%password"
smbclient -L //<IP> -U "domain\\user%password"

# Connect to a share
smbclient //<IP>/share -N
smbclient //<IP>/share -U "user%password"

# Inside smbclient session
ls                          # list files
cd folder
get file.txt                # download
put localfile.txt           # upload
recurse ON; prompt OFF; mget *   # recursive download
```

---

# smbmap

```bash
# Anonymous / null session
smbmap -H <IP>
smbmap -H <IP> -u '' -p ''

# With credentials
smbmap -H <IP> -u user -p password
smbmap -H <IP> -u user -p password -d DOMAIN

# Recursive listing
smbmap -H <IP> -R
smbmap -H <IP> -R share

# Download / Upload
smbmap -H <IP> --download 'share\path\file.txt'
smbmap -H <IP> --upload '/local/file.txt' 'share\remote\file.txt'
```

---

# enum4linux / enum4linux-ng

```bash
# Classic
enum4linux -a <IP>
enum4linux -a -u "" -p "" <IP>
enum4linux -a -u guest -p "" <IP>

# Modern version (recommended)
enum4linux-ng -A <IP>
enum4linux-ng -A -u user -p password <IP>

# Specific options
enum4linux -U <IP>          # Users
enum4linux -S <IP>          # Shares
enum4linux -G <IP>          # Groups
enum4linux -P <IP>          # Password policy
enum4linux -r <IP>          # RID cycling
```

---

# rpcclient

```bash
# Null session
rpcclient -U "" -N <IP>
rpcclient -U "%" <IP>

# With credentials
rpcclient -U "user%password" <IP>

# Useful commands inside rpcclient
enumdomusers
enumdomgroups
queryuser <RID>
querygroup <RID>
querydominfo
netshareenumall
lookupnames username
lookupsids S-1-5-21-...
getusername
```

---

# **NetBIOS: nbtstat / nmblookup**

```bash
nbtstat -A 10.10.10.5               # Windows-native NetBIOS name enumeration
nmblookup -A 10.10.10.5             # Linux equivalent (Samba suite)
```

---

# Nmap SMB Scripts

```bash
nmap --script smb-os-discovery -p445 10.10.10.5
nmap --script smb-enum-shares -p445 10.10.10.5
nmap --script smb-enum-users -p445 10.10.10.5
nmap --script smb-vuln* -p445 10.10.10.5           # check known SMB vulnerabilities
nmap --script smb-protocols -p445 10.10.10.5       # check SMB version support (SMBv1 detection)
```