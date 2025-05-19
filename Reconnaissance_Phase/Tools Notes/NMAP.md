# Cheat Sheet to NMAP for Reconnaissance

<b>NMAP (Network Mapper)</b> is one of the most powerful and widely used tools for network reconnaissance and security auditing. This guide covers everything you need to know about using NMAP effectively during the reconnaissance phase of security assessments.

---

## What is NMAP ?
<b>NMAP is an open-source utility for network discovery and security auditing.</b> Created by Gordon Lyon (also known as Fyodor), it's designed to rapidly scan large networks or single hosts to determine:

- Available hosts on a network
- Services (ports) those hosts are offering
- Operating systems they're running
- Types of packet filters/firewalls in use
- And dozens of other characteristics

---

## Why Use NMAP ?
1. **Comprehensive Network Mapping**: Quickly identify all devices connected to a network
2. **Service Enumeration**: Discover what services are running on target systems
3. **Vulnerability Assessment**: Identify potential security weaknesses based on open ports and services
4. **OS Detection**: Determine operating systems to tailor exploitation attempts
5. **Firewall/IDS Evasion**: Test network security controls
6. **Baseline Creation**: Establish a network baseline for future comparison
7. **Efficiency**: Automate discovery that would be impractical to perform manually.

---

## When to Use NMAP
1. **Initial Reconnaissance**: At the beginning of a penetration test to identify targets
2. **Network Auditing**: Regular security assessments of your infrastructure
3. **System Administration**: Verifying network configurations and changes
4. **Incident Response**: Identifying unauthorized devices or services
5. **Compliance Checks**: Verifying that only authorized services are exposed
6. **Before Major Changes**: Understanding the current network state before modifications
---

### Basic Syntax

<b>The basic syntax for NMAP is:</b>
```bash
nmap [scan type] [options] {target specification}
```

### Common Scan Types:
<b>Simple Scan of Target</b>
```bash
nmap 192.168.1.1 [Example-Target]
```

### Network Scan:
<b>Scan Entire Subnet</b>
```bash
nmap 192.168.1.1/24 [Example-Target]
```

### OS Scan:
<b>Identify Operating System</b>
```bash
nmap -O 192.168.1.1 [Example-Target]
```

### Service Version Detection:
<b>Determine versions of running services:</b>
```bash
nmap -sV 192.168.1.1 [Example-Target]
```

### Comprehensive Scan
<b>Combine multiple scan types for thorough reconnaissance:</b>

```bash
nmap -sS -sV -sC -A -O -p- 192.168.1.1 [Example-Target]
```
---
## 🔧 Advanced Nmap Techniques

| **Type**               | **Description**                                             | **Command**                                                      |
|------------------------|-------------------------------------------------------------|------------------------------------------------------------------|
| **Timing Template**    | Control scan speed (0-5, where 0 is slowest and 5 is fastest) | `nmap -T4 192.168.1.1`                                           |
| **Script Scanning**    | Use NSE (Nmap Scripting Engine) for advanced vulnerability scanning | `nmap --script=vuln 192.168.1.1`                         |
| **Evasion Techniques** | Avoid detection by IDS/IPS systems                           | `nmap -f -T0 -n -Pn --data-length 200 -D RND:10 192.168.1.1`     |
| **Output Options**     | Save results in different formats                            | `nmap -oA scan_results 192.168.1.1`                              |

---

![Host Discovery](https://raw.githubusercontent.com/neelvaria/Ethical_Hacking_Notes/master/Reconnaissance_Phase/Images/HostDiscovery.png)


Here's what a basic host discovery scan looks like:

```shellscript
nmap -sn 192.168.1.0/24
```

This produces output showing which hosts are up:

```plaintext
Starting Nmap 7.92 ( https://nmap.org ) at 2023-05-19 10:03 EDT
Nmap scan report for 192.168.1.1
Host is up (0.0023s latency).
Nmap scan report for 192.168.1.5
Host is up (0.0046s latency).
Nmap scan report for 192.168.1.10
Host is up (0.0018s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 2.25 seconds
```