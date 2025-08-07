# :material-security: Hack The Box Write‑ups

Welcome to my comprehensive collection of **Hack The Box (HTB)** machine write-ups. Each writeup documents a complete attack chain from initial enumeration to privilege escalation, with detailed explanations of *why* every step works.

!!! tip "What Makes These Different"
    These writeups focus on **manual exploitation techniques** and **understanding the underlying vulnerabilities** rather than just running automated tools. Each step includes the reasoning behind the approach and alternative methods when applicable.

---

## :material-map: How to Navigate

=== "Quick Start"
    1. **Browse machines** by difficulty in the sidebar
    2. **Use the search function** (top-right) for specific tools, CVEs, or techniques
    3. **Check the Resources section** for methodology and tool references

=== "Writeup Structure"
    Each writeup follows this consistent format:
    
    - **Synopsis** — Key facts, difficulty, and learning objectives
    - **Enumeration** — Port scanning, service discovery, and reconnaissance  
    - **Foothold** — Initial access method and vulnerability exploitation
    - **Privilege Escalation** — Path to administrative access
    - **Lessons Learned** — Key takeaways, references, and remediation

=== "Advanced Usage"
    - **Filter by difficulty** using the navigation tabs
    - **Copy commands** directly from code blocks (hover for copy button)
    - **Follow attack paths** with visual flow diagrams where applicable

---

## :material-server: Current Write‑ups

| Difficulty | Machine | Attack Path | Key Techniques |
|:----------:|---------|-------------|----------------|
| <span class="difficulty-badge difficulty-easy">Easy</span> | [Sau](Sau/Sau.md) | SSRF → Maltrail RCE → sudo privesc | CVE-2023-27163, Command injection, systemctl pager escape |

<div class="attack-path">
<strong>Coming Soon:</strong> More machines across all difficulty levels with focus on modern vulnerabilities and attack techniques.
</div>

---

## :material-target: Methodology Overview

<div class="writeup-step">
<div class="step-number">1</div>
<div>
<strong>Reconnaissance & Enumeration</strong><br>
Comprehensive <span class="tool-highlight">nmap</span> scanning, service enumeration, and technology fingerprinting
</div>
</div>

<div class="writeup-step">
<div class="step-number">2</div>
<div>
<strong>Vulnerability Analysis</strong><br>
Manual testing, CVE research, and exploit development/modification
</div>
</div>

<div class="writeup-step">
<div class="step-number">3</div>
<div>
<strong>Exploitation & Access</strong><br>
Gaining initial foothold through identified vulnerabilities
</div>
</div>

<div class="writeup-step">
<div class="step-number">4</div>
<div>
<strong>Post-Exploitation</strong><br>
System enumeration, credential harvesting, and privilege escalation
</div>
</div>

<div class="writeup-step">
<div class="step-number">5</div>
<div>
<strong>Documentation & Remediation</strong><br>
Comprehensive writeup with screenshots, code, and security recommendations
</div>
</div>

---

## :material-information: About

These writeups are created for **educational purposes** to help security professionals understand attack methodologies and improve defensive strategies. All activities are performed in controlled lab environments.

!!! warning "Ethical Use"
    The techniques documented here should only be used in authorized testing environments or your own lab setups. Always obtain proper permission before testing any systems.

---

<div style="text-align: center; margin-top: 2em; color: var(--md-default-fg-color--light);">
<em>Maintained by Mohamed Trigui • Last updated: January 2024</em>
</div>
