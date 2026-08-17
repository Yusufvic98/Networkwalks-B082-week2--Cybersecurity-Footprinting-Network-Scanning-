
# Networkwalks-B082-week2--Cybersecurity-Footprinting-Network-Scanning-

Week 2 penetration testing reports (NetworkWalks internship) — OSINT Footprinting with theHarvester & Network Scanning with Zenmap/Nmap.

**Electives (BOTH REQUIRED):**
- `W2-PM4` — theHarvester-based Footprinting Attacks
- `W2-PM5` — Zenmap-based Network Scanning
- `W2-PM-FINAL` — Detailed report covering both modules

---

## 📌 Overview

This repository documents Week 2 of my Cybersecurity & Ethical Hacking internship at **NetworkWalks (Batch B082)**. It covers two practical modules:

1. **Module 1 — Footprinting & Reconnaissance:** passive OSINT gathering against a public domain using `theHarvester`.
2. **Module 2 — Network Scanning:** active host discovery on an isolated lab network using `Zenmap` (Nmap GUI).

The full write-up — methodology, evidence, risk analysis, and recommendations — is compiled in the final report: [`NetworkWalks_Week2_Report.pdf`](./NetworkWalks_Week2_Report.pdf).

---

## 🧰 Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux 2026.1 (VirtualBox) | Operating system for both modules |
| theHarvester v4.10.1 | OSINT aggregation — emails, subdomains, hosts, IPs, ASNs |
| Zenmap (Nmap 7.991 GUI) | Host discovery on the local lab subnet |

---

## 🕵️ Module 1 — Footprinting with theHarvester (W2-PM4)

**Objective:** Passively collect publicly available information about a target domain (`microsoft.com`) without directly interacting with its live infrastructure.

**Steps taken:**
1. Reviewed the tool's help menu (`theHarvester -h`) to confirm available flags and OSINT source list.
2. Ran a single-source scan against a known search engine:
   ```
   theHarvester -d microsoft.com -l 1000 -b baidu
   ```
3. Ran a full-source scan across every source theHarvester supports:
   ```
   theHarvester -d microsoft.com -l 50 -b all
   ```
4. Recorded which premium/API-gated sources failed due to missing API keys (Shodan, VirusTotal, Censys, SecurityTrails, BuiltWith, etc.) and which free sources succeeded (Baidu, CRTsh, Certspotter, DuckDuckGo, Hackertarget, Hudson Rock, Wayback Machine, and others).
5. Analyzed the results: harvested emails, discovered subdomains/hosts (including pre-production `-dev`/`-test`/`-uat`/`-ppe` naming patterns), IP ranges, and ASNs.
6. Flagged notable findings — large external attack surface, exposed staging hosts, and legacy/typo DNS records — for the risk analysis section of the report.

**Key results:**
- 3 emails harvested per scan
- 4 ASNs identified
- 119 IP addresses identified
- 9,951 subdomains/hosts identified (all-sources scan)

---

## 🌐 Module 2 — Network Scanning with Zenmap (W2-PM5)

**Objective:** Identify live hosts on an isolated lab network before proceeding to port/service enumeration.

**Steps taken:**
1. Identified the lab subnet (`192.168.56.0/24` — a VirtualBox host-only network).
2. Opened Zenmap and ran a host-discovery (ping) scan:
   ```
   nmap -sn 192.168.56.0/24
   ```
3. Reviewed the **Nmap Output** tab to confirm live hosts, their IP addresses, and MAC addresses.
4. Cross-referenced MAC address vendor prefixes to confirm the hosts were VirtualBox virtual NICs, consistent with the expected lab topology.
5. Documented the scan as **discovery-only** (no port/service data captured) and noted follow-up port scanning (`-sV -sC -p-`) as the next step.

**Key results:**
- 256 addresses scanned, 3 hosts live
- Host IPs and MAC addresses recorded for the host machine + 2 guest VMs
- Scan completed in 5.24 seconds

---

## 📄 Report

The complete `W2-PM-FINAL` report — combining both modules with a liability disclaimer, tools table, activities performed, color-coded risk analysis, recommendations, and conclusion — is available here:

📥 [**NetworkWalks_Week2_Report.pdf**](./NetworkWalks_Week2_Report.pdf)

---

## ⚠️ Disclaimer

All activities in this repository were performed only against publicly available OSINT sources or my own isolated lab environment. This work is for educational purposes only as part of the NetworkWalks internship program. No unauthorized access or testing was performed against any live system.

---

## 👤 Author

**Oyewumi Yusuf Olayemi**
Cybersecurity Intern — NetworkWalks Internship Program (Batch B082)
📧 Yusufvic98@gmail.com
