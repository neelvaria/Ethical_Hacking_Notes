## Index

1. [Introduction](#introduction)
2. [Key Features](#key-features)
3. [Installation](#installation)
4. [User Interface Overview](#user-interface-overview)
5. [Capturing Packets](#capturing-packets)
6. [Filters](#filters)
    - [Capture Filters](#capture-filters)
    - [Display Filters](#display-filters)
7. [Protocol Analysis](#protocol-analysis)
8. [Common Use Cases](#common-use-cases)
9. [Tips & Best Practices](#tips--best-practices)
10. [Security Considerations](#security-considerations)
11. [Wireshark Command Examples](#wireshark-command-examples)
12. [Resources](#resources)
13. [Conclusion](#conclusion)

---

## Introduction

**Wireshark** is a free and open-source packet analyzer used for network troubleshooting, analysis, software and communications protocol development, and education. It is widely regarded as the de facto standard for network protocol analysis.

## Key Features

- **Packet Capture**: Captures live network data from Ethernet, Wi-Fi, Bluetooth, and more.
- **Deep Inspection**: Analyses hundreds of protocols, with more added regularly.
- **Live and Offline Analysis**: View data in real-time or open previously saved capture files.
- **Rich Display Filters**: Powerful filtering capabilities to focus on relevant traffic.
- **Export Options**: Export data to various formats (CSV, XML, JSON, plain text).
- **Color Coding**: Customizable coloring rules for quick visual analysis.
- **VoIP Analysis**: Specialized tools for analyzing Voice over IP traffic.
- **Cross-Platform**: Available for Windows, macOS, and Linux.

## Installation

- **Windows**: Download installer from [Wireshark.org](https://www.wireshark.org/).
- **macOS**: Available via Homebrew (`brew install wireshark`) or direct download.
- **Linux**: Install via package manager (e.g., `sudo apt install wireshark`).

---

## User Interface Overview

- **Menu Bar**: Access to file, edit, view, capture, analyze, statistics, and help options.
- **Main Toolbar**: Quick access to common actions (open, save, start/stop capture).
- **Packet List Pane**: Displays captured packets with summary info.
- **Packet Details Pane**: Hierarchical view of protocol layers for selected packet.
- **Packet Bytes Pane**: Raw data in hexadecimal and ASCII.
- **Status Bar**: Capture status, filters, and statistics.

## Capturing Packets

1. **Select Network Interface**: Choose the interface to capture traffic from.
2. **Start Capture**: Click the "Shark Fin" icon or `Capture > Start`.
3. **Apply Capture Filters (optional)**: Limit captured data (e.g., `tcp port 80`).
4. **Stop Capture**: Click the red square icon or `Capture > Stop`.
5. **Save Capture**: File > Save As (`.pcap` or `.pcapng` format).

**Reference Screenshot: Capture Interfaces Dialog**

![Wireshark Capture Interfaces](https://raw.githubusercontent.com/neelvaria/Ethical_Hacking_Notes/master/Reconnaissance_Phase/Images/wsmain.png)
*Figure: Wireshark Capture Interfaces Dialog* 

---

## Filters

### Capture Filters

- Applied before capturing, limits what is recorded.
- Syntax is similar to tcpdump.
- **Examples**:
  - Capture only HTTP: `tcp port 80`
  - Capture traffic from IP: `host 192.168.1.1`
  - Capture only TCP: `tcp`

### Display Filters

- Applied after capture, for viewing specific packets.
- More powerful and flexible than capture filters.
- **Examples**:
  - Show only HTTP: `http`
  - Show packets from IP: `ip.src == 192.168.1.1`
  - Show TCP SYN packets: `tcp.flags.syn == 1 && tcp.flags.ack == 0`

**Reference Screenshot: Filter Toolbar**

![Wireshark Filter Toolbar](https://raw.githubusercontent.com/neelvaria/Ethical_Hacking_Notes/master/Reconnaissance_Phase/Images/ws_filter.png)
*Figure: Wireshark Filter Toolbar for entering display filters* 

---

## Protocol Analysis

- **Protocol Hierarchy**: `Statistics > Protocol Hierarchy` shows protocol breakdown.
- **Follow Streams**: Right-click a TCP/UDP packet > "Follow TCP/UDP Stream" to view conversation.
- **Reassembly**: Wireshark can reassemble fragmented packets for easier analysis.

---
## Common Use Cases

- **Troubleshooting Network Issues**: Identify latency, dropped packets, or retransmissions.
- **Security Analysis**: Detect suspicious traffic, malware, or unauthorized access.
- **Protocol Development**: Debug and verify custom or standard protocol implementations.
- **Performance Analysis**: Measure throughput, latency, and network utilization.
- **Educational Purposes**: Learn about network protocols and packet structures.

---
## Tips & Best Practices

- **Run as Administrator/Root**: Required for capturing on some interfaces.
- **Limit Capture Size**: Use filters or set capture limits to avoid large files.
- **Anonymize Data**: Use Wireshark's tools to remove sensitive information before sharing captures.
- **Update Regularly**: New protocol support and bug fixes are released frequently.
- **Use Coloring Rules**: Highlight important traffic for faster analysis.

---
## Security Considerations

- **Sensitive Data**: Captures may contain passwords, cookies, or personal data.
- **Legal Compliance**: Ensure you have permission to capture network traffic.
- **Malicious Traffic**: Be cautious when opening captures from untrusted sources.

---

#### Summary Table

| Command Example                                      | Description                                    |
|------------------------------------------------------|------------------------------------------------|
| `wireshark -i eth0`                                  | Capture on eth0                                |
| `wireshark -i eth0 -k -f "tcp port 443"`             | Capture HTTPS traffic on eth0                  |
| `wireshark -i eth1 -a duration:300 -w capture.pcap`  | Capture 5 minutes on eth1, save to file        |
| `wireshark -r file.pcap -Y "http"`                   | Open capture file, show only HTTP packets      |
| `tshark -i eth0 -f "port 53" -w dns_traffic.pcap`    | Terminal capture DNS traffic, save to file     |

---

## Resources

- **Official Website**: [https://www.wireshark.org/](https://www.wireshark.org/)
- **User Guide**: [Wireshark User’s Guide](https://www.wireshark.org/docs/wsug_html_chunked/)
- **Sample Captures**: [Wireshark Sample Captures](https://wiki.wireshark.org/SampleCaptures)
- **Display Filter Reference**: [Wireshark Display Filter Reference](https://www.wireshark.org/docs/dfref/)

---

## Conclusion

> Wireshark is a powerful tool for anyone working with networks, from beginners to experts. Mastering its features can significantly enhance your ability to analyze, troubleshoot, and secure network communications.

---
