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

### 2. Custom Word Lists for DNS Brute Force
You can use custom word lists for DNS brute force by modifying the wordlists in the `wordlists` directory.

### 3. Proxy Configuration
To use theHarvester with a proxy:

```bash
# Set HTTP proxy environment variable
export HTTP_PROXY="http://proxy.example.com:8080"
export HTTPS_PROXY="http://proxy.example.com:8080"

# Then run theHarvester
theHarvester -d example.com -b google
```

### 4. Automating with Shell Scripts
Create a script to automate reconnaissance across multiple domains:

```bash
#!/bin/bash
# File: recon.sh

domains=("example.com" "example.org" "example.net")
sources="google,bing,linkedin,dnsdumpster,certspotter"

for domain in "${domains[@]}"; do
  echo "Gathering information for $domain"
  theHarvester -d "$domain" -l 500 -b "$sources" -f "$domain-results"
  echo "Completed $domain"
  echo "-----------------------"
done
```

## Output Interpretation
> theHarvester provides results in several categories:

### 1. Emails
- These are email addresses associated with the target domain.

### 2. Hosts
- These are subdomains and hostnames associated with the target domain.

### 3. IP Addresses
- IP addresses associated with discovered hosts.

### 4. Virtual Hosts
- Virtual hosts running on the same IP address.

### 5. Shodan Results
- If using Shodan as a source, you'll get information about open ports and services.

### 6. DNS Names
- Additional DNS names discovered through various techniques.

## Integration with Other Tools
- theHarvester works well as part of a larger reconnaissance workflow:

### 1. Piping to Other Tools
```bash
# Extract subdomains and pipe to Nmap
theHarvester -d example.com -b all | grep -Eo '([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.example\.com' | sort -u > subdomains.txt
nmap -iL subdomains.txt
```

### 2. Integration with Maltego
- theHarvester results can be imported into Maltego for visual analysis.


### 3. Combining with Other OSINT Tools
```bash
# Combine with Sublist3r
theHarvester -d example.com -b all > harvester_results.txt
sublist3r -d example.com -o sublist3r_results.txt

# Combine results
cat harvester_results.txt sublist3r_results.txt | sort -u > combined_results.txt
```

## Best Practices

1. **Legal Considerations**: Only use theHarvester on domains you own or have explicit permission to test.
2. **Rate Limiting**: Be mindful of rate limits, especially when using search engines as sources.
3. **API Key Management**: Keep your API keys secure and don't share them in public repositories.
4. **Comprehensive Approach**: Use multiple sources for the most complete results.
5. **Verification**: Always verify the information gathered before acting on it.
6. **Documentation**: Document your findings and methodology for future reference.
7. **Stealth**: For sensitive engagements, consider using proxies or VPNs to avoid detection.
---

# 🛠️ Troubleshooting Guide for theHarvester
## 🔧 Common Issues and Solutions

### 1. **Rate Limiting**

- **Issue**:  
  *"Google has blocked your IP due to too many requests"*

- **Solution**:  
  Wait before making more requests, use a VPN, or switch to alternative sources.

---

### 2. **API Key Errors**

- **Issue**:  
  *"Invalid API key for [source]"*

- **Solution**:  
  Verify your API key is correct and properly configured in the `api-keys.yaml` file.

---

### 3. **No Results**

- **Issue**:  
  *No results returned for a domain*

- **Solution**:  
  Try different sources, check your internet connection, or verify the domain exists.

---

### 4. **Installation Problems**

- **Issue**:  
  *Dependencies fail to install*

- **Solution**:
  ```bash
  pip install --upgrade pip
  pip install -r requirements.txt --ignore-installed
  ```
### 5. Python Version Compatibility

- **Issue:**
  *"Requires Python 3.7"*

- **Solution:**
  Update your Python version or use a virtual environment with a compatible version.
---

```bash
# Basic usage
theHarvester -d example.com -l 500 -b google

# Comprehensive scan
theHarvester -d example.com -l 1000 -b all -c -t

# Email harvesting focus
theHarvester -d example.com -l 500 -b google,bing,yahoo,linkedin

# Subdomain enumeration focus
theHarvester -d example.com -b dnsdumpster,certspotter,crtsh,sublist3r,bufferoverun

# Save results to file
theHarvester -d example.com -b all -f results

# DNS brute force
theHarvester -d example.com -c -b google

# Search with Google dorks
theHarvester -d example.com -g -b google

# Search for exposed passwords
theHarvester -d example.com -p -b google

# Perform reverse DNS lookups
theHarvester -d example.com -b google -r

# Use specific DNS server
theHarvester -d example.com -b google -e 8.8.8.8

# TLD expansion
theHarvester -d example -t

# Verify hostnames via DNS resolution
theHarvester -d example.com -b google -v
```


## Conclusion

**theHarvester is an essential tool in any security professional's arsenal for passive reconnaissance.** By leveraging multiple data sources, it provides valuable insights into an organization's digital footprint without directly interacting with their systems.

Remember to use this tool ethically and responsibly, always ensuring you have proper authorization before conducting any information gathering activities.

---

> ⚠️ Disclaimer: This guide is provided for educational and legitimate security testing purposes only. Always obtain proper authorization before performing reconnaissance activities on any systems or networks you do not own.
---