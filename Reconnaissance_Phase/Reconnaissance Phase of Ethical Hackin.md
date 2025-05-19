# Reconnaissance Phase of Ethical Hacking Methodology

This README provides comprehensive notes and reference material for the Reconnaissance (Footprinting) phase in the Ethical Hacking methodology. It covers theory, techniques, tools, commands, workflows, and countermeasures.

---

## Table of Contents
1. [Overview](#overview)
2. [Objectives](#objectives)
3. [Passive Reconnaissance Techniques](#passive-reconnaissance-techniques)
4. [Active Reconnaissance Techniques](#active-reconnaissance-techniques)
5. [Key Tools & Frameworks](#key-tools--frameworks)
6. [Reconnaissance Workflow](#reconnaissance-workflow)
7. [Common Recon Scripts & Commands](#common-recon-scripts--commands)
8. [Information to Record](#information-to-record)
9. [Countermeasures & Defenses](#countermeasures--defenses)
10. [Ethical & Legal Aspects](#ethical--legal-aspects)
11. [Summary Comparison](#summary-comparison)

---

## Overview

- **Definition**: First phase (Footprinting) where information about a target (organization, system, network) is collected.
- **Goal**: Build a detailed target profile to identify possible vulnerabilities before launching active attacks.
- **Categories**:
  - **Passive Reconnaissance**: No direct interaction; low risk of detection.
  - **Active Reconnaissance**: Direct probing of systems; higher risk of detection.

## Objectives

1. **Identify Targets**: Domain names, IP ranges, subdomains.
2. **Discover Technology Stack**: OS, web servers, frameworks, CMSs.
3. **Map Network Infrastructure**: Firewalls, routers, load balancers.
4. **Gather Personnel Info**: Emails, employee names, roles.
5. **Uncover Publicly Exposed Data**: Code repos, leaked credentials, backups.

## Passive Reconnaissance Techniques

| **Technique**                 | **Description**                                          | **Example Command / URL**                             |
|---------------------------|------------------------------------------------------|-----------------------------------------------------|
| WHOIS Lookup              | Domain registrar, ownership, DNS servers             | `whois example.com`                                 |
| DNS Enumeration           | Retrieve DNS records                                 | `dig +short example.com any`<br>`host -a example.com`|
| Web Archive Mining        | Historical snapshots of sites                        | https://archive.org                                 |
| Search Engine Dorking     | Advanced queries for exposed data                    | `site:example.com filetype:pdf \"password\"`      |
| Certificate Transparency  | Find subdomains via public SSL cert logs             | `https://crt.sh/?q=%25.example.com`                 |
| Social Media Profiling    | Harvest employee info, tech, org structure           | LinkedIn, Twitter                                   |
| Job Postings              | Reveal tech stack, software versions                 | Corporate careers page                              |
| Public Code Repositories  | Search for committed credentials/configs             | `github.com/example \"password =\"`                |

## Active Reconnaissance Techniques

| Technique            | Purpose                               | Tool / Command                                                  |
|----------------------|---------------------------------------|-----------------------------------------------------------------|
| Ping Sweep           | Identify live hosts                   | `nmap -sn 192.168.1.0/24`                                       |
| Port Scanning        | Discover open ports & services        | `nmap -sV -p 1-65535 example.com`                               |
| Version Detection    | Determine software versions           | `nmap -sV example.com`                                          |
| OS Detection         | Identify operating system             | `nmap -O example.com`                                           |
| Traceroute           | Map network path                      | `traceroute example.com` (Linux)<br>`tracert example.com` (Win) |
| Banner Grabbing      | Extract service banners               | `nc example.com 80` → send `HEAD / HTTP/1.0`                    |
| SNMP Enumeration     | Query devices via SNMP                | `snmpwalk -c public -v1 10.0.0.1`                               |
| SMB Enumeration      | List shares & users on Windows hosts  | `enum4linux -a 10.0.0.5`                                        |

## Key Tools & Frameworks

### Passive Recon Tools
- **theHarvester**:
  ```bash
  theharvester -d example.com -l 200 -b google
  ```
- **Recon-ng**:
  ```bash
  recon-ng
  modules load recon/domains-hosts/google_site_web
  set SOURCE example.com
  run
  ```
- **Maltego** – Graph-based OSINT analysis.
- **Shodan** – Internet-of-Things device search.
- **Censys** – Public internet scan data.

### Active Recon Tools
- **Nmap** – Network discovery and security auditing.
- **Masscan** – High-speed port scanner.
- **Netcat (nc)** – Banner grabbing, raw TCP/UDP connections.
- **Metasploit auxiliary scanners** – Integrated port & service scanning.

## Reconnaissance Workflow

1. **Define Scope & Rules of Engagement**: Authorized IPs/domains; prohibited actions.
2. **Gather Passive Data**: WHOIS → DNS → OSINT → code repositories.
3. **Analyze & Correlate**: Map findings; identify high-value assets.
4. **Plan Active Scans**: Select port ranges; schedule to avoid detection.
5. **Execute Active Probes**: Ping sweeps → Port scans → Banner grabs.
6. **Document & Report**: Record commands, outputs, timestamps, and potential issues.

## Common Recon Scripts & Commands

```bash
# WHOIS and DNS
whois target.com

# DNS records
dig +short target.com any

# Subdomain enumeration via crt.sh
curl -s "https://crt.sh/?q=%.target.com" | grep target.com

# Ping sweep + quick port scan
nmap -Pn -T4 --min-rate=1000 -p1-1000 10.10.10.0/24

# Service & OS detection
nmap -sS -sV -O -p22,80,443 target.com

# HTTP banner grab
echo -e "HEAD / HTTP/1.0\n\n" | nc target.com 80

# SNMP enumeration
snmpwalk -c public -v2c target.com

# SMB enumeration
enum4linux -a target.com
```

## Information to Record

- **Target Identifiers**: IP, hostname, domain.
- **Open Ports & Services**: Port/service/version.
- **OS & Device Types**: Linux, Windows, routers, printers.
- **Network Topology**: Subnets, gateways.
- **Potential Entry Points**: Exposed RDP, outdated services.
- **Human Elements**: Employee emails, org charts.

## Countermeasures & Defenses
1. **Minimize Information Exposure**: Disable DNS zone transfers; clean up DNS records.
2. **Harden Services**: Patch software; disable default banners.
3. **Implement IDS/IPS**: Monitor unusual scan patterns.
4. **Network Segmentation**: Isolate critical assets in VLANs.
5. **Secure SNMP/SMB**: Use strong community strings; disable SMBv1.
6. **Rate-Limit & VPN Access**: Throttle external requests; require VPN for management.

## Ethical & Legal Aspects

- Obtain **written authorization** (signed rules-of-engagement).
- Remain within agreed scope and timeframes.
- Preserve evidence and maintain **chain of custody** if needed.
- Report findings responsibly without exploiting vulnerabilities.

## Summary Comparison

| Aspect             | Passive Recon              | Active Recon                   |
|--------------------|-----------------------------|--------------------------------|
| **Detection Risk**     | Very low                    | Moderate to high               |
| **Data Depth**         | Surface-level (public)      | Deep (service versions)        |
| **Typical Tools**      | OSINT frameworks, search    | Nmap, Netcat, Masscan          |
| **Legal Concerns**     | Minimal (public data only)  | Higher (network probing)       |

---