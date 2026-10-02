# NETWORKWALKS-B083-WK4-PM1-2-3-4-Penetration-Testing-Project
Blackbox pentest on Mediroza Hospital 
# Mediroza Hospital — Penetration Testing Engagement

**Author:** Makaranga Praise (B083)
**Program:** Networkwalks Cybersecurity Internship
**Target:** `medirozahospital.com` (authorized training environment)
**Status:** Completed — Milestones 1–4

> ⚠️ **Disclaimer:** This project was conducted in a controlled environment for educational purposes only, against a target explicitly authorized for security testing by Networkwalks. All techniques documented here were performed with **written permission** from the client and must never be applied to any system without explicit authorization from its owner.

---

## 📋 Overview

This repository documents a full black-box penetration test against a simulated hospital web application and infrastructure, carried out as part of the Networkwalks Cybersecurity Internship. The engagement progressed through four milestones: reconnaissance, enumeration, exploitation of a critical data exposure, and a formal written report.

## 🎯 Scope

- **Primary target:** `medirozahospital.com` (199.188.201.16)
- **Hosting:** Shared hosting (web-hosting.com / cPanel-style environment), fronted by HAProxy + LiteSpeed
- **Authorization:** Written permission granted prior to testing — see engagement report for full terms

## 🗂️ Milestones

| Milestone | Objective | Outcome |
|---|---|---|
| M1 | Reconnaissance | WHOIS, DNS enumeration, port/service scanning, web fingerprinting, WAF detection |
| M2 | Enumeration | Mapped exposed services and web paths |
| M3 | Critical data exposure | SQL injection auth bypass → PHI exposure → DB backup disclosure |
| M4 | Reporting | Full penetration testing report delivered |

## 🔍 Key Findings Summary

| # | Finding | Risk |
|---|---|---|
| 1 | `robots.txt` discloses sensitive directory names | Low |
| 2 | Directory listing enabled on `/old/`, `/patient/`, `/staff/` | High |
| 3 | SQL injection authentication bypass on patient portal login | **Critical** |
| 4 | Exposure of patient PHI (pathology reports) via portal | **Critical** |
| 5 | Weak/crackable encryption on "protected" PDF reports | High |
| 6 | Publicly accessible full database backup (staff salaries + shareholder records) | **Critical** |
| 7 | Exposed PHP application error log | Medium |

Full technical detail, proof-of-exploitation evidence, CVSS-style risk justification, and remediation guidance for each finding is in the complete report: **[`Mediroza_Pentest_Report_M4.docx`](./Mediroza_Pentest_Report_M4.docx)**.

## 🛠️ Tools Used

- **Recon/enumeration:** `nmap`, `whois`, `nslookup`, `dnsrecon`, `whatweb`, `wafw00f`, `curl`
- **Exploitation:** Manual SQL injection testing (tautology-based auth bypass)
- **Password cracking:** John the Ripper (`pdf2john.pl`, `rockyou.txt`), Networkwalks Hash Calculator & Password Cracker
- **File/metadata analysis:** `exiftool`, `qpdf`, `pdftotext`

## 🧭 Methodology

Testing followed a standard black-box methodology aligned with PTES / OWASP Testing Guide phases:

1. **Reconnaissance** — passive and active information gathering
2. **Enumeration** — service banners, directory/robots.txt discovery
3. **Vulnerability identification** — authentication logic and injection testing
4. **Exploitation** — auth bypass, file retrieval, offline credential recovery
5. **Post-exploitation analysis** — review of exposed data for sensitive classes

## ✅ Recommendations (high level)

- Patch the SQL injection via parameterized queries / prepared statements
- Disable directory indexing on all web-accessible paths
- Remove backup files from the web root; store backups in access-controlled storage
- Replace password-protected PDFs with authenticated, access-controlled document delivery
- Restrict public access to application log files
- Establish recurring penetration testing and a secure SDLC process

See the full report for the complete immediate / short-term / long-term remediation roadmap.

## 📁 Repository Contents

```
├── Mediroza_Pentest_Report_M4.docx   # Full penetration testing report
├── evidence/                         # Screenshots and raw tool output (recon, exploitation, cracking)
└── README.md                         # This file
```

## 🔒 Responsible Disclosure Note

Sensitive personal data uncovered during this engagement (e.g. national ID numbers, contact details, full database backup) is **not included in this repository** or in the main report body, in line with responsible handling of exposed data. That material is retained separately as restricted engagement evidence and shared only with the instructor as required.

---

*This project is for educational purposes only, completed under the Networkwalks Cybersecurity Academy training program.*
