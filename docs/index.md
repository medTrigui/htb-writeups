# Hack The Box Write‑ups

Welcome to my curated archive of Hack The Box (HTB) machine write‑ups.  Each report is designed to be **self‑contained** and **reproducible**, showcasing a complete attack chain from enumeration to privilege escalation while explaining *why* every step works.

> **Disclosure note :** Only **retired** HTB machines are published here, in line with the platform’s rules.

---

## 1  How to Navigate this Repository

1. **Pick a machine** from the left‑hand sidebar (or the list below).
2. **Follow the numbered sections** inside the write‑up:
   1. Synopsis – key facts at a glance
   2. Enumeration – ports, services, and initial findings
   3. Foothold – gaining the first shell
   4. Privilege Escalation – method and exploit
   5. Lessons Learned / References
3. **Use the built‑in search** (top‑right) to jump to commands, CVEs, or tools.

---

## 2  Current Write‑ups

| Difficulty | Machine           | Attack Path                                         |  Status |
| ---------: | ----------------- | --------------------------------------------------- | :-----: |
|       Easy | [Sau](Sau/Sau.md) | SSRF → Maltrail 0.53 RCE → `systemctl` pager escape |    ✅    |

<!-- Add rows here as new write‑ups are published. -->

---

## 3  Planned Additions

1. **Forest (Windows AD, Medium)** – Kerberoasting & domain privilege escalation.
2. **Fluffy (Linux, Easy)** – Web exploitation + sudo misconfig.
3. **Buffer‑Overflow Lab** – Custom exploit against VulnServer (*prep for OSCP*).

---

## 4  Methodology Snapshot

1. **Enumeration :**  `nmap`, `rustscan`, service‑specific scripts.
2. **Exploitation :**  Prefer manual payloads; Metasploit only when noted.
3. **Post‑Exploitation :**  Proof of Concept, flag capture, and clean‑up.
4. **Documentation :**  Screenshots at critical milestones, code blocks with exact commands, and links to official advisories.

---

*Maintained by Mohamed Trigui – last update: `2025‑05‑28`.*

