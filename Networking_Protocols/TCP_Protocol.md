
# Transmission Control Protocol (TCP) – Comprehensive Notes

## 📌 Overview

TCP (Transmission Control Protocol) is a **connection-oriented**, **reliable**, **byte-stream** transport protocol. It is one of the core protocols of the Internet Protocol Suite, operating at the **Transport Layer** of the OSI model.

## 🔑 Key Features

- **Connection-Oriented:** Requires a connection to be established before data transfer.
- **Reliable Delivery:** Uses acknowledgment (ACKs) and retransmissions.
- **Flow Control:** Uses a sliding window mechanism.
- **Congestion Control:** Implements algorithms to avoid network congestion.
- **Ordered Delivery:** Ensures data is delivered in the same order it was sent.
- **Full-Duplex Communication:** Simultaneous two-way data transmission.

## TCP Header Format

![TCP Header Format](https://raw.githubusercontent.com/neelvaria/Ethical_Hacking_Notes/master/Networking_Protocols/Images/TCP_Header.jpg)


| Field                     | Size (bits) | Description                              |
|---------------------------|-------------|------------------------------------------|
| Source Port               | 16          | Port of sender                           |
| Destination Port          | 16          | Port of receiver                         |
| Sequence Number           | 32          | Number of the first data byte            |
| Acknowledgment Number     | 32          | Next expected byte from sender           |
| Data Offset               | 4           | Header length                            |
| Reserved                  | 3           | Reserved for future use                  |
| Flags (Control Bits)      | 9           | URG, ACK, PSH, RST, SYN, FIN             |
| Window Size               | 16          | Buffer size of receiver                  |
| Checksum                  | 16          | Error-checking of header and data        |
| Urgent Pointer            | 16          | Indicates urgent data                    |
| Options                   | Variable    | Used for features like MSS, Window Scale |
| Padding                   | Variable    | Ensures header is a multiple of 32 bits  |

## 📚 TCP Flags

- **SYN** – Synchronize (used in connection establishment)
- **ACK** – Acknowledgment field is significant
- **FIN** – No more data from sender (connection termination)
- **RST** – Reset the connection
- **PSH** – Push Function (data should be sent immediately)
- **URG** – Urgent Pointer field is significant

## 🔄 Connection Establishment (3-Way Handshake)

![TCP 3-Way Handshake](https://raw.githubusercontent.com/neelvaria/Ethical_Hacking_Notes/master/Networking_Protocols/Images/3-Way_Handshake_🤝.webp)

1. **SYN:** Client sends SYN to server.
2. **SYN-ACK:** Server responds with SYN-ACK.
3. **ACK:** Client sends ACK, connection established.

## 🔁 Connection Termination (4-Way Handshake)

![TCP 4-Way Handshake](https://raw.githubusercontent.com/neelvaria/Ethical_Hacking_Notes/master/Networking_Protocols/Images/4-Way_Handshake_🤝.png)

1. **FIN:** Sender wants to close connection.
2. **ACK:** Receiver acknowledges.
3. **FIN:** Receiver sends FIN.
4. **ACK:** Sender acknowledges, connection closed.

## 📤 Flow Control – Sliding Window

![TCP Sliding Window](https://upload.wikimedia.org/wikipedia/commons/3/3c/Sliding_window.svg)

- Prevents sender from overwhelming receiver.
- Window size advertised by receiver.
- Adjusts dynamically based on receiver buffer availability.

## 🌐 Congestion Control Algorithms

![TCP Congestion Control](https://upload.wikimedia.org/wikipedia/commons/3/3c/TCP_congestion_control.svg)

1. **Slow Start**
2. **Congestion Avoidance**
3. **Fast Retransmit**
4. **Fast Recovery**

TCP uses **AIMD (Additive Increase Multiplicative Decrease)** strategy to adjust the congestion window.

## 🧪 Error Detection

- TCP uses a **16-bit checksum** to detect errors in the header and data.

## 🧠 Sequence and Acknowledgment

- **Sequence Number:** Used to identify data segments.
- **Acknowledgment Number:** Confirms receipt of data.

## 📦 Maximum Segment Size (MSS)

- MSS defines the largest amount of data a device can receive in a single TCP segment.
- Negotiated during the connection setup.

## 🔄 Retransmission Mechanism

- **Timeout-based retransmission**
- **Duplicate ACKs (Fast Retransmit)**

## 📊 Common TCP Ports

| Protocol         | Port Number |
|------------------|-------------|
| HTTP             | 80          |
| HTTPS            | 443         |
| FTP (Control)    | 21          |
| SSH              | 22          |
| Telnet           | 23          |
| SMTP             | 25          |
| POP3             | 110         |

## 🔍 Comparison: TCP vs UDP

| Feature         | TCP                         | UDP                         |
|-----------------|-----------------------------|-----------------------------|
| Type            | Connection-oriented         | Connectionless              |
| Reliability     | Reliable (ACK, retransmit)  | Unreliable                  |
| Ordering        | Ensured                     | Not guaranteed              |
| Speed           | Slower                      | Faster                      |
| Use Cases       | Web, Email, FTP, SSH        | DNS, VoIP, Streaming        |

## 📘 Use Cases of TCP

- Web Browsing (HTTP/HTTPS)
- File Transfers (FTP, SFTP)
- Emails (SMTP, IMAP, POP3)
- Secure Shell (SSH)
- Remote Desktop (RDP)

## 🎥 Recommended Video Resource

[![TCP Congestion Control](https://img.youtube.com/vi/cIHiSR4j3g4/0.jpg)](https://www.youtube.com/watch?v=cIHiSR4j3g4)

*Source: [YouTube - TCP Congestion Control](https://www.youtube.com/watch?v=cIHiSR4j3g4)*

*Note: The images used are sourced from Wikipedia and are available under the Creative Commons license.*
