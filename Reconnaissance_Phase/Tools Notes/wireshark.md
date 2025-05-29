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

![Wireshark Capture Interfaces](https://github.com/neelvaria/Ethical_Hacking_Notes/blob/master/Reconnaissance_Phase/Images/wsmain.png)
*Figure: Wireshark Capture Interfaces Dialog* 

---