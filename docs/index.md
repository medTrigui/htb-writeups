# Hack The Box Write‑ups
Welcome to my repository of Hack The Box (HTB) machine write-ups. Each entry is documented with a complete attack chain from enumeration to privilege escalation while explaining *why* every step works.

---

## 1  How to Navigate this Repository

1. **Pick a machine** from the left‑hand sidebar (or the list below).

2. **Follow the numbered sections** inside each write‑up:

   - **Synopsis —** key facts
   - **Enumeration —** ports, services, and initial findings
   - **Foothold —** gaining the first shell
   - **Privilege Escalation —** method and exploit
   - **Lessons Learned / References**

3. **Use the built‑in search** (top‑right) to jump directly to commands, CVEs, or tools.


---

## 2  Current Write‑ups

| Difficulty | Machine           | Attack Path                                             |
| ---------: | ----------------- | ------------------------------------------------------- |
|       Easy | [Sau](Sau/Sau.md) | SSRF --> Maltrail 0.53 RCE --> `systemctl` pager escape |  

<!-- Add rows here as new write‑ups are published. -->

---

## 4  Methodology Snapshot

1. **Enumeration :**  `nmap`.
2. **Exploitation :**  I prefer crafting manual payloads and analyzing CVE-related exploit scripts. I only rely on Metasploit when needed.
3. **Post‑Exploitation :**  Privilege Escalation and root access.
4. **Documentation :**  Screenshots, code blocks, and links to official advisories.

---

*Maintained by Mohamed Trigui – last update: `2025‑05‑28`.*
