# Week 2 - Footprinting & Network Scanning (W2-PM-FINAL)

Penetration testing lab report for the **Networkwalks Cybersecurity & Ethical Hacking Program** (Batch B082), Week 2.

| | |
|---|---|
| **Pentester** | Muhammad Yaqoob (MYMB) |
| **Program** | Cybersecurity program at Networkwalks |
| **Modules** | W2-PM1 (Multiple Kali Tools), W2-PM5 (Zenmap Scanning) |
| **Dates** | 10-13 November 2026 |
| **Phases covered** | Phase 1: Reconnaissance & Footprinting, Phase 2: Scanning & Network Discovery |

## Disclaimer

All activities were performed only on systems where I had written permission (Networkwalks, as part of the program) or on systems I own (my own lab networks). This material is for education and research only. Do not use it to break the law. Unauthorised access is a crime in most countries, even when nothing is damaged.

## What this report covers

### 1. Footprinting (W2-PM1) - target: `networkwalks.com`

| Tool | What it was used for | Main observation |
|---|---|---|
| `whois` | Domain registration details | Registrar GoDaddy; created 6 Nov 2019; expires 6 Nov 2027; owner hidden by privacy service; DNSSEC unsigned |
| `whatweb` | Web technology fingerprint | Apache, WordPress 7.1.4, WordPress Download Manager 3.3.76, IP 192.232.216.135 |
| `nslookup` | DNS resolution | Domain resolves to 192.232.216.135 |
| `curl -I` | HTTP response headers | HTTP/2 200, `/wp-json/` REST API link exposed, HTTP redirects to HTTPS; HSTS and other security headers not seen |
| `wafw00f` | WAF detection | ModSecurity (SpiderLabs) detected |

### 2. Network scanning (W2-PM5) - target: my own lab networks

- `ipconfig` on Windows identified `192.168.56.1/24` and `169.254.141.170/16`.
- Zenmap ping scans (`nmap -sn`) of both Windows addresses found 1 host up each.
- Zenmap ping scan of `10.0.0.0/24` from Kali Linux reported 256 of 256 hosts up in 67.81 seconds. This includes the network and broadcast addresses, so the result is probably not 256 real devices and needs verification.
- A scan of `255.255.255.0` (the subnet mask) by mistake returned 0 hosts up. The target must be an IP address or range such as `192.168.56.0/24`.
- Zenmap Topology view of the 10.0.0.0/24 scan was captured.

## Risk summary

The report lists 7 observations (2 Medium, 5 Low). These are **observations, not confirmed vulnerabilities**. No exploitation or vulnerability validation was performed in these two modules.

## Environment

- Kali Linux in Oracle VirtualBox (Nmap 7.99)
- Windows PC with Zenmap (Nmap 7.80) and PowerShell

## Repository contents

```
.
├── README.md
├── W2-PM-FINAL_Report_Muhammad_Yaqoob.docx   # Final report
├── evidence/                                  # Screenshots used in the report
│   ├── task1_ss1.jpg, task1_ss2.jpg           # WHOIS
│   ├── task2.jpg                              # WhatWeb
│   ├── task3.jpg                              # Nslookup
│   ├── task4.jpg                              # Curl headers
│   ├── task5.jpg                              # Wafw00f
│   ├── zenmap_task2.jpg                       # ipconfig
│   ├── zenmap_.jpg, zenmap_4_.jpg             # Windows ping scans
│   ├── zenmap_task1.jpg, zenmap_3.jpg         # Kali ping scan of 10.0.0.0/24
│   ├── task7.jpg, Screenshot_2026-11-13_103228.jpg   # Topology
│   └── zenmap_task3.jpg                       # Wrong-target scan (255.255.255.0)
└── subnets.txt                                # Saved Nmap output (256 hosts)
```

> Note: the saved Nmap output was originally named `subnets.xlsx`, but it is a plain text file. Rename it to `subnets.txt` before uploading.

## What I learned

- How much public information can be collected about a target before any exploitation.
- How to read WHOIS, WhatWeb, curl header and WAF results, and what each means for an attacker.
- How to find my own IP address and subnet, and how to run and read a Zenmap ping scan.
- Scan results must be verified. A long list of "hosts up" does not always mean real devices.
- Always enter the correct target and always stay within an authorised scope.

## Author

**Muhammad Yaqoob (MYMB)** - Cybersecurity student and Networkwalks program intern
LinkedIn: https://www.linkedin.com/in/muhammad-yaqoob-843822302
