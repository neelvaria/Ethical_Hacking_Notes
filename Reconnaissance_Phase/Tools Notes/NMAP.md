# 🛠️ Cheat Sheet to **Nmap** for Reconnaissance

**🔍 Nmap (Network Mapper)** is one of the most powerful and widely used tools for **network reconnaissance** and **security auditing**. This guide covers everything you need to know to use Nmap effectively during the **reconnaissance phase** of security assessments.
---

## What is Nmap❓

**🧰 Nmap is an open-source utility for network discovery and security auditing.**  
Created by **Gordon Lyon** (aka *Fyodor*), it’s designed to rapidly scan large networks or single hosts to determine:

- Available hosts on a network  
- Services (ports) those hosts are offering  
- Operating systems they're running  
- Types of packet filters/firewalls in use  
- And many more characteristics...

---
## 💡 Why Use Nmap?

1. **Comprehensive Network Mapping** – Quickly identify all devices connected to a network  
2. **Service Enumeration** – Discover what services are running on target systems  
3. **Vulnerability Assessment** – Detect potential weaknesses based on open ports and services  
4. **OS Detection** – Determine operating systems to tailor your approach  
5. **Firewall/IDS Evasion** – Test how well the network defends itself  
6. **Baseline Creation** – Establish normal network behavior  
7. **Efficiency** – Automate discovery processes that would be time-consuming manually

---

## 🕒 When to Use Nmap ?
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

```basg
nmap -sn 192.168.1.0/24
```

This produces output showing which hosts are up:

```bash
Starting Nmap 7.92 ( https://nmap.org ) at 2023-05-19 10:03 EDT
Nmap scan report for 192.168.1.1
Host is up (0.0023s latency).
Nmap scan report for 192.168.1.5
Host is up (0.0046s latency).
Nmap scan report for 192.168.1.10
Host is up (0.0018s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 2.25 seconds
```
---
### Example 2: Port Scanning

A typical port scan output looks like this:

```bash
Starting Nmap 7.92 ( https://nmap.org ) at 2023-05-19 10:05 EDT
Nmap scan report for target-server.local (192.168.1.10)
Host is up (0.0054s latency).
Not shown: 995 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
3306/tcp open  mysql
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 1.20 seconds
```
---
### Example 3: Service Version Detection

```bash
nmap -sV 192.168.1.10
```

Output:

```bash
Starting Nmap 7.92 ( https://nmap.org ) at 2023-05-19 10:07 EDT
Nmap scan report for target-server.local (192.168.1.10)
Host is up (0.0065s latency).
Not shown: 995 closed ports
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http     Apache httpd 2.4.41 ((Ubuntu))
443/tcp  open  ssl/http Apache httpd 2.4.41 ((Ubuntu))
3306/tcp open  mysql    MySQL 8.0.28-0ubuntu0.20.04.3
8080/tcp open  http     Jetty 9.4.39.v20210325

Nmap done: 1 IP address (1 host up) scanned in 11.64 seconds
```
---
### Example 4: OS Detection

```bash
nmap -O 192.168.1.10
```

Output:

```bash
Starting Nmap 7.92 ( https://nmap.org ) at 2023-05-19 10:10 EDT
Nmap scan report for target-server.local (192.168.1.10)
Host is up (0.0072s latency).
Not shown: 995 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
3306/tcp open  mysql
8080/tcp open  http-proxy
Device type: general purpose
Running: Linux 5.X
OS CPE: cpe:/o:linux:linux_kernel:5.4
OS details: Linux 5.4
Network Distance: 2 hops

Nmap done: 1 IP address (1 host up) scanned in 3.62 seconds
```
---
### Example 5: Comprehensive Scan with NSE Scripts

```bash
nmap -sS -sV -sC -A -p- 192.168.1.10
```
This produces detailed output including:

- All open ports (even non-standard ones)
- Service versions
- OS detection
- Traceroute information
- Default script scan results
---

## NMAP Scan Types

<b>Here's a quick reference of common scan types:</b>

| Flag | Scan Type | Description
|-----|-----|-----
| **-sS** | SYN Scan | Half-open scanning, doesn't complete TCP connections
| **-sT** | TCP Connect | Complete TCP connection scanning
| **-sU**| UDP Scan | Scans for open UDP ports
| **-sA** | ACK Scan | Used to map firewall rulesets
| **-sV** | Version Detection | Determines service versions
| **-O** | OS Detection | Identifies operating system
| **-sC** | Script Scan | Runs default NSE scripts
| **-sn** | Ping Scan | Host discovery without port scanning
| **-p-** | All Ports | Scans all 65535 ports
---

## ⚡ Port Scanning Techniques

| Command              | Description             |
|----------------------|--------------------------|
| `-p 22,80,443`        | ****Specific ports**** to scan |
| `-p 1-1000`           | Scan ****port range**** |
| `-p-`                | Scan ****all ports (1-65535)**** |
| `-p http,https`       | Use ****service names**** |
| `-p T:22,U:53`        | Protocol-specific scan |
| `-F`                 | ****Fast scan**** (top 100 ports) |
| `--top-ports 1000`    | Scan top N ports |
| `-p-65535`           | Include ****port 0**** in scan |

---

## 🔍 Service/Version Detection

| Command                         | Description              |
|---------------------------------|---------------------------|
| `-sV`                           | ****Service version**** detection |
| `--version-intensity 0-9`       | Set probe intensity level |
| `--version-light`               | Use fewer probes |
| `--version-all`                 | Try all available probes |
| `-A`                            | ****Aggressive scan**** (includes OS detection, version detection, script scanning)

---

## 💻 OS Detection

| Command                | Description               |
|------------------------|----------------------------|
| `-O`                   | Enable ****OS detection**** |
| `--osscan-limit`       | Limit OS detection to promising targets |
| `--osscan-guess`       | Aggressive OS guessing |
| `--max-os-tries 1`     | Set max tries for OS detection |

---

## ⏱️ Timing & Performance

| Command                    | Description                        |
|----------------------------|-------------------------------------|
| `-T0` to `-T5`             | Timing templates (****T4 is default****) |
| `--min-rate 100`           | Minimum packets per second         |
| `--max-rate 100`           | Maximum packets per second         |
| `--min-parallelism 10`     | Minimum probes parallelism         |
| `--max-parallelism 10`     | Maximum probes parallelism         |
| `--min-rtt-timeout 1s`     | Minimum probe timeout              |
| `--max-rtt-timeout 10s`    | Maximum probe timeout              |
| `--host-timeout 30m`       | Timeout per host                   |
| `--scan-delay 1s`          | Delay between probe packets        |

---

## 💾 Output Options

| Command             | Description              |
|---------------------|---------------------------|
| `-oN file.txt`       | Normal human-readable output |
| `-oX file.xml`       | XML output                |
| `-oG file.gnmap`     | Grepable output           |
| `-oA filename`       | ****All formats saved**** with base name |
| `-v`, `-vv`          | Increase verbosity        |
| `--reason`           | Show reason for port state |
| `--open`             | Show only ****open**** ports |
| `--packet-trace`     | Display sent/received packets |
| `--resume file.xml`  | Resume a paused scan      |

---

## 🧠 NSE Scripting

| Command                | Description              |
|------------------------|---------------------------|
| `-sC` or `--script=default` | Run ****default scripts**** |
| `--script=vuln`         | Run known vulnerability detection scripts |
| `--script=safe`         | Run non-intrusive scripts |
| `--script=auth`         | Authentication check scripts |
| `--script=banner`       | Banner grabbing           |
| `--script-args=arg=val` | Pass arguments to script  |
| `--script-updatedb`     | Update the NSE database   |

---

## 🛡️ Firewall / IDS Evasion

| Command                   | Description               |
|---------------------------|----------------------------|
| `-f`, `-f -f`              | ****Fragment packets**** (evasion) |
| `-D RND:10`               | Use ****random decoys**** |
| `-S IP_Address`           | Spoof source IP           |
| `--data-length 200`       | Append random data        |
| `--ttl 64`                | Set TTL                   |
| `--spoof-mac MAC`         | Spoof MAC address         |
| `--badsum`, `--adler32`   | Send bad checksums        |
| `--proxies`               | Proxy chaining            |

---

## ⚙️ Common Examples

| Command                                       | Description             |
|-----------------------------------------------|--------------------------|
| `nmap 192.168.1.1`                             | Basic scan               |
| `nmap -sS -sV -O 192.168.1.1`                  | ****Comprehensive scan**** |
| `nmap -p- 192.168.1.1`                         | All ports                |
| `nmap -sU -sS 192.168.1.1`                     | TCP and UDP scan         |
| `nmap -sn 192.168.1.0/24`                      | ****Ping sweep**** for live hosts |
| `nmap -A -T4 192.168.1.1`                      | Aggressive scan          |
| `nmap -sV --script=vuln 192.168.1.1`           | Vulnerability detection  |
| `nmap -sS -sV -D RND:10 192.168.1.1`           | Stealth decoy scan       |
| `nmap -sS -p 1-65535 -T4 -A -v 192.168.1.1`    | ****Full aggressive scan**** |
| `nmap -sS -sV -O -oA scan 192.168.1.1`         | Save all outputs         |

---

## 🧩 Practical Workflows

| Step               | Command                                       |
|--------------------|-----------------------------------------------|
| Host Discovery     | `nmap -sn 192.168.1.0/24`                     |
| Quick Scan         | `nmap -T4 -F 192.168.1.1`                     |
| Detailed Scan      | `nmap -sS -sV -p- -T4 -A 192.168.1.1`         |
| Vulnerability Scan | `nmap --script vuln 192.168.1.1`             |
| Stealth Scan       | `nmap -sS -T2 --data-length 200 192.168.1.1` |

---
## 🛠️ Nmap Basic Command Cheatsheet
```bash
# Basic scan
nmap 192.168.1.1

# Scan specific ports
nmap -p 22,80,443 192.168.1.1

# Scan port ranges
nmap -p 1-1000 192.168.1.1

# Scan all 65535 ports
nmap -p- 192.168.1.1

# Scan using service name
nmap -p http,https 192.168.1.1

# Scan multiple targets
nmap 192.168.1.1 192.168.1.2 192.168.1.3

# Scan from a file
nmap -iL targets.txt

# Scan a subnet
nmap 192.168.1.0/24

# Aggressive scan
nmap -A 192.168.1.1

# Save output to all formats
nmap -oA scan_results 192.168.1.1
```

## 📌 Notes

- ****Always run Nmap with root/administrator privileges**** for full features.
- Use `-Pn` when host discovery is blocked by firewall (no ping).
- Combine multiple options for maximum insight.
- Be ethical—get proper authorization before scanning!
---

## 📷 Images & Diagrams

> 🖼️ If you want to embed images from GitHub:
- Upload the image inside the repository
- Use the **raw** GitHub link: