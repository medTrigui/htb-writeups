# Methodology

This page outlines the systematic approach used for HTB machine writeups.

---

## General Approach

### 1. Reconnaissance & Enumeration
- **Port Scanning**: `nmap` with various flags for comprehensive service detection
- **Service Enumeration**: Detailed analysis of running services
- **Web Application Testing**: Directory busting, technology identification
- **Version Detection**: Identifying software versions for vulnerability research

### 2. Vulnerability Research
- **CVE Database Search**: Using identified versions to find known vulnerabilities
- **Exploit Database**: Searching for available exploits
- **Manual Testing**: Testing for common misconfigurations

### 3. Initial Access
- **Exploit Development**: Crafting or modifying existing exploits
- **Manual Exploitation**: Leveraging web application vulnerabilities
- **Social Engineering**: If applicable (rare in HTB)

### 4. Post-Exploitation
- **System Enumeration**: Understanding the compromised system
- **Credential Harvesting**: Searching for credentials and sensitive data
- **Privilege Escalation**: Escalating to higher privileges

### 5. Persistence & Documentation
- **Maintaining Access**: If required for the engagement
- **Screenshot Documentation**: Capturing proof of compromise
- **Report Generation**: Comprehensive writeup with remediation advice

---

## Tools Used

### Reconnaissance
- **Nmap**: Network discovery and security auditing
- **Masscan**: Fast port scanner
- **Rustscan**: Fast port scanner written in Rust

### Web Application Testing
- **Gobuster**: Directory/file enumeration
- **Ffuf**: Fast web fuzzer
- **Burp Suite**: Web application security testing platform
- **OWASP ZAP**: Web application security scanner

### Exploitation
- **Metasploit**: Penetration testing framework
- **Custom Scripts**: Tailored exploits for specific vulnerabilities
- **Manual Techniques**: Direct command injection, SQL injection, etc.

### Post-Exploitation
- **LinEnum**: Linux enumeration script
- **winPEAS**: Windows privilege escalation awesome script
- **GTFOBins**: Unix binaries that can be exploited for privilege escalation

---

## Documentation Standards

Each writeup follows this structure:

1. **Synopsis**: Machine overview, difficulty, and key learning points
2. **Enumeration**: Detailed reconnaissance and service analysis  
3. **Foothold**: Initial access method and exploitation
4. **Privilege Escalation**: Path to administrative access
5. **Lessons Learned**: Key takeaways and references

---

## Ethical Guidelines

- All activities are performed in controlled lab environments
- No real-world systems are targeted without explicit permission
- Knowledge is shared for educational and defensive purposes
- Responsible disclosure practices are followed for any discovered vulnerabilities