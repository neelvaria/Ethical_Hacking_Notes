
# Detailed Notes on HTTP & HTTPS Protocol

## 📑 Index

1. [Introduction](#-1-introduction)
2. [What is HTTP?](#-2-what-is-http)
3. [What is HTTPS?](#-3-what-is-https)
4. [SSL/TLS Overview](#️-4-ssltls-overview)
5. [HTTP Methods](#-5-http-methods)
6. [HTTP vs HTTPS - Detailed Comparison](#-6-http-vs-https---detailed-comparison)
7. [Why Use HTTPS?](#️-7-why-use-https)
8. [Related Terms](#-8-related-terms)
9. [How to Identify HTTPS in Browser](#-9-how-to-identify-https-in-browser)
10. [Mnemonics to Remember](#-10-mnemonics-to-remember)
11. [Summary](#-11-summary)
12. [Final Note](#-12-final-note)
---

## 1. Introduction

HTTP and HTTPS are both protocols used for transmitting hypertext (web) data between a client (usually a web browser) and a server. The main difference lies in the way the data is transmitted—HTTPS adds security features using encryption.

---

## 2. What is HTTP?

###  Definition

HTTP stands for **HyperText Transfer Protocol**. It is an application-layer protocol used for transmitting hypermedia documents, such as HTML. It is the foundation of any data exchange on the Web.

###  Characteristics

- **Stateless:** Each request from a client is independent of previous requests.
- **Connectionless:** The client initiates a request, the server processes it and disconnects.
- **Text-based:** Requests and responses are readable.
- **Unsecured:** Data is sent as plain text, making it vulnerable to interception.

### Default Port
- **Port 80**

###  HTTP Versions

| Version | Features |
|---------|----------|
| HTTP/0.9 | Simple protocol, only GET method |
| HTTP/1.0 | Introduced POST and status codes |
| HTTP/1.1 | Persistent connections, chunked transfers |
| HTTP/2   | Binary framing, multiplexing, header compression |
| HTTP/3   | Based on QUIC protocol, faster and secure |

###  HTTP Request Structure

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

###  HTTP Response Structure

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 305

<html>...</html>
```

---

## 3. What is HTTPS?

###  Definition

**HTTPS** stands for **HyperText Transfer Protocol Secure**. It is the secure version of HTTP. It uses **SSL/TLS protocols** to encrypt data transmission, ensuring privacy and data integrity.

###  Key Components

- **SSL/TLS:** Protocol used to encrypt communication.
- **Digital Certificate (X.509):** Issued by Certificate Authorities (CAs) to validate domain ownership.
- **Handshake Process:** Exchange of keys before encrypted data transfer.

###  Default Port
- **Port 443**

###  HTTPS Workflow

1. Client connects to the server via HTTPS.
2. Server sends a digital certificate.
3. Client verifies the certificate with the CA.
4. Secure symmetric key is exchanged using asymmetric encryption.
5. Encrypted communication begins.

---

## 4. SSL/TLS Overview

| Component       | Description |
|----------------|-------------|
| SSL            | Secure Sockets Layer (now deprecated) |
| TLS            | Transport Layer Security (used in HTTPS today) |
| Cipher Suites  | Defines the encryption, key exchange, and MAC algorithms |
| Certificates   | Verify the identity of the website |
| CA             | Certificate Authority, a trusted third party |

---

## 5. HTTP Methods

| Method   | Description |
|----------|-------------|
| GET      | Requests data from the server |
| POST     | Sends data to the server |
| PUT      | Updates existing resource |
| DELETE   | Deletes a specified resource |
| HEAD     | Same as GET but returns only headers |
| OPTIONS  | Returns allowed HTTP methods |
| PATCH    | Partially updates a resource |

---

## 6. HTTP vs HTTPS - Detailed Comparison

| Feature           | HTTP                         | HTTPS                          |
|------------------|------------------------------|--------------------------------|
| Full Form        | HyperText Transfer Protocol  | HyperText Transfer Protocol Secure |
| Port             | 80                           | 443                            |
| Security         | Unsecured                    | Encrypted using SSL/TLS        |
| Encryption       | None                         | End-to-end encryption          |
| Certificate      | Not required                 | Requires SSL/TLS certificate   |
| SEO              | Neutral                      | SEO-boosted by Google          |
| Trust Indicator  | No padlock icon              | Padlock icon in browser        |
| Performance      | Slightly faster              | Slight overhead due to encryption |
| Use Case         | Public/non-sensitive data    | Secure login, payments, private data |

---

## 7. Why Use HTTPS?

-  Secures communication
-  Protects user data (login, payments)
-  Prevents MITM (Man-in-the-middle) attacks
-  Increases website trust and credibility
-  Required for PCI DSS (Payment Card Industry Data Security Standard) compliance
-  Google Chrome marks HTTP sites as **Not Secure**

---

## 8. Related Terms

| Term               | Description |
|--------------------|-------------|
| SSL Certificate    | Proves website’s identity and enables HTTPS |
| TLS                | Current standard protocol for HTTPS |
| CA (Cert Authority)| Issues trusted certificates |
| MITM Attack        | Intercepting and altering data between client and server |
| PKI                | Public Key Infrastructure used for certificate management |

---

## 9. How to Identify HTTPS in Browser

- 🔒 Padlock icon before URL
- `https://` prefix in address bar
- Option to view certificate details in browser settings

---

## 10. Mnemonics to Remember

- **HTTP:** "Hackers Try To Peek"
- **HTTPS:** "Hackers Terminated via Padlock Securely"
- **SSL/TLS:** "Secure Socket Layer / Transport Layer Security"

---

## 11. Summary

| Criteria     | HTTP                      | HTTPS                         |
|--------------|---------------------------|-------------------------------|
| Protocol     | Application Layer         | Application Layer with TLS    |
| Data Format  | Plaintext                 | Encrypted                     |
| Suitable For | Non-sensitive websites    | All modern websites, especially with logins or transactions |

---

## 12. Final Note

Always prefer **HTTPS** when deploying websites. It protects both you and your users. You can get free SSL certificates from services like [Let’s Encrypt](https://letsencrypt.org).

---
