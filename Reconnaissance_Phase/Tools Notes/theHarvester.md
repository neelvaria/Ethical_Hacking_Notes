## 🕵️ The Harvester: Comprehensive Guide
### 📑 Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Basic Usage](#basic-usage)
- [Command Options](#command-options)
- [Data Sources](#data-sources)
- [Common Use Cases](#common-use-cases)
- [Advanced Techniques](#advanced-techniques)
- [Output Interpretation](#output-interpretation)
- [Integration with Other Tools](#integration-with-other-tools)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)


## 🕵️ Introduction

**theHarvester is an open-source intelligence (OSINT) tool** designed for early-stage penetration testing and red team engagements. It helps security professionals gather information about a target organization by collecting:

- Email addresses
- Subdomains
- Virtual hosts
- Open ports
- Employee names & more...


theHarvester achieves this by querying multiple public data sources, search engines, and APIs to create a comprehensive profile of an organization's digital footprint.

## ⚙️ Installation

### Prerequisites
- Python 3.7+
- pip (Python package manager)

### Method 1: Using pip
```bash
pip install theHarvester
```

### Method 2: From GitHub repository
```bash
# Clone the repository
git clone https://github.com/laramies/theHarvester.git

# Navigate to the directory
cd theHarvester

# Install requirements
pip install -r requirements.txt

# Install the package
python setup.py install
```

### Method 3: Using Docker
```bash
# Pull the Docker image
docker pull laramies/theharvester

# Run theHarvester in a container
docker run -it laramies/theharvester
```

### Method 4: Using Kali Linux
theHarvester comes pre-installed on Kali Linux. To update to the latest version:

```bash
apt update
apt install theharvester
```

## Basic Usage
The basic syntax for theHarvester is:

```bash
theHarvester -d <domain> -l <limit> -b <source>
```

### Simple Example
```bash
theHarvester -d example.com -l 500 -b google
```

> *This command searches for information related to "example.com" using Google as the data source, with a limit of 500 results.*

## Command Options
theHarvester offers numerous command-line options:
```bash
# Basic options
-d DOMAIN      Target domain to search
-l LIMIT       Limit the number of results (default: 500)
-S START       Start with result number X (default: 0)
-g             Use Google dorking for additional information
-p             Use Google dorking to search for exposed passwords
-s             Start with result number X (default: 0)

# Source selection
-b SOURCE      Data source: google, bing, bingapi, bufferoverun, certspotter, etc.
-f FILE        Save output to HTML and XML files
-h             Show help message and exit

# DNS options
-c             Perform DNS brute force on the domain
-t             Perform DNS TLD expansion discovery
-r             Perform reverse DNS lookup on results
-n             Perform DNS lookup on found subdomains
-e DNS_SERVER  Specify DNS server to use for lookups

# Output options
-o FILE        Save output to XML file
-v             Verify host names via DNS resolution
```

## 🌐 Data Sources
*theHarvester can query multiple data sources:*
| **Source**           | **Description**                        | **API Key Required** |
|----------------------|----------------------------------------|----------------------|
| **anubis**           | Anubis-DB                              | No                   |
| **baidu**            | Baidu search engine                    | No                   |
| **bing**             | Bing search engine                     | No                   |
| **bingapi**          | Bing search API                        | Yes                  |
| **bufferoverun**     | BufferOverrun.com                      | No                   |
| **censys**           | Censys.io                              | Yes                  |
| **certspotter**      | Cert Spotter                           | No                   |
| **crtsh**            | crt.sh Certificate search              | No                   |
| **dnsdumpster**      | DNSdumpster.com                        | No                   |
| **duckduckgo**       | DuckDuckGo search engine               | No                   |
| **fullhunt**         | Fullhunt.io                            | Yes                  |
| **github-code**      | GitHub code search                     | Yes                  |
| **google**           | Google search engine                   | No                   |
| **hackertarget**     | HackerTarget.com                       | No                   |
| **hunter**           | Hunter.io                              | Yes                  |
| **intelx**           | IntelligenceX                          | Yes                  |
| **linkedin**         | LinkedIn                               | No                   |
| **netcraft**         | Netcraft Data Mining                   | No                   |
| **otx**              | AlienVault Open Threat Exchange        | Yes                  |
| **pentesttools**     | Pentest-Tools.com                      | Yes                  |
| **projectdiscovery** | ProjectDiscovery.io                    | No                   |
| **qwant**            | Qwant search engine                    | No                   |
| **rapiddns**         | RapidDNS.io                            | No                   |
| **securityTrails**   | SecurityTrails                         | Yes                  |
| **shodan**           | Shodan                                 | Yes                  |
| **spyse**            | Spyse.com                              | Yes                  |
| **sublist3r**        | Sublist3r                              | No                   |
| **threatcrowd**      | ThreatCrowd                            | No                   |
| **threatminer**      | ThreatMiner                            | No                   |
| **trello**           | Trello                                 | No                   |
| **twitter**          | Twitter                                | Yes                  |
| **urlscan**          | URLScan.io                             | Yes                  |
| **virustotal**       | VirusTotal                             | Yes                  |
| **yahoo**            | Yahoo search engine                    | No                   |
| **zoomeye**          | ZoomEye                                | Yes                  |



### Using Multiple Sources
You can specify multiple sources by separating them with commas:

```bash
theHarvester -d example.com -b google,bing,linkedin
```

To use all available sources:
```bash
theHarvester -d example.com -b all
```

## 📌 Common Use Cases
### 1. Basic Email Harvesting
```bash
theHarvester -d company.com -l 500 -b google,bing,yahoo
```

### 2. Finding Subdomains
```bash
theHarvester -d company.com -b dnsdumpster,sublist3r,certspotter,crtsh
```

### 3. DNS Brute Force
```bash
theHarvester -d company.com -c -b google
```

### 4. TLD Expansion
```bash
theHarvester -d company -t
```

### 5. Searching for Exposed Credentials
```bash
theHarvester -d company.com -g -p
```

### 6. Comprehensive Information Gathering
```bash
theHarvester -d company.com -l 1000 -b all -c -t -r -n
```

## Advanced Techniques
### 1. Using API Keys
For sources that require API keys, create a `api-keys.yaml` file in the config directory:

```yaml
apikeys:
  bing:
    key: "your_bing_api_key_here"
  github:
    key: "your_github_api_key_here"
  hunter:
    key: "your_hunter_api_key_here"
  securitytrails:
    key: "your_securitytrails_api_key_here"
  shodan:
    key: "your_shodan_api_key_here"
```

