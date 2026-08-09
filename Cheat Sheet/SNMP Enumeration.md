# SNMP Enumeration

Platform: General
Status: Solid
Tags: Enumeration
Type: cheat sheet

# Community String Brute-Forcing

```bash
# onesixtyone (fast & recommended)
onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt <IP>
onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt <IP>

# Common default strings to try first
public
private
manager
community
snmp
admin
```

---

# snmpwalk

```bash
# Full MIB walk (v1 and v2c)
snmpwalk -c public -v1 <IP>
snmpwalk -c public -v2c <IP>
snmpwalk -c private -v1 <IP>

# Make output human-readable (important!)
sudo apt install snmp-mibs-downloader
sudo download-mibs
# Then edit /etc/snmp/snmp.conf and comment out the "mibs :" line
```

---

# Most Useful OIDs

| OID | Description | Command Example |
| --- | --- | --- |
| 1.3.6.1.2.1.1 | System information | `snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.1` |
| 1.3.6.1.4.1.77.1.2.25 | **Windows Users** | `snmpwalk -c public -v1 <IP> 1.3.6.1.4.1.77.1.2.25` |
| 1.3.6.1.2.1.25.4.2.1.2 | **Running Processes** | `snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.25.4.2.1.2` |
| 1.3.6.1.2.1.25.6.3.1.2 | **Installed Software** | `snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.25.6.3.1.2` |
| 1.3.6.1.2.1.6.13.1.3 | **Open TCP Ports** | `snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.6.13.1.3` |
| 1.3.6.1.2.1.25.1.6.0 | System Processes count | `snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.25.1.6.0` |
| 1.3.6.1.2.1.4.22.1.2 | ARP Table | `snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.4.22.1.2` |

---

# snmp-check

```bash
snmp-check <IP>
snmp-check -t <IP> -c public
snmp-check -t <IP> -c private
```

---

# Nmap SNMP Scripts

```bash
sudo nmap -sU -p 161 --script snmp-info,snmp-sysdescr <IP>
sudo nmap -sU -p 161 --script snmp-processes <IP>
sudo nmap -sU -p 161 --script snmp-win32-users <IP>
sudo nmap -sU -p 161 --script snmp-win32-services <IP>
sudo nmap -sU -p 161 --script snmp-win32-shares <IP>
sudo nmap -sU -p 161 --script snmp-netstat <IP>
sudo nmap -sU -p 161 --script "snmp-*" <IP>
```