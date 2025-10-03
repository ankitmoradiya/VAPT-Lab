# 🛡️ VAPT Lab Workshop - Quick Reference Guide

## 📋 Prerequisites
- Docker & Docker Compose installed
- Git installed
- Basic command line knowledge

---

## 🚀 Setup Instructions

### 1. Clone Repository
```bash
git clone https://github.com/ankitmoradiya/Workshop2025.git
cd Workshop2025/VAPT\ Lab/
```

### 2. Launch Lab Environment
```bash
# Build container
docker-compose build

# Start container
docker-compose up -d

# Access lab shell
docker exec -it vapt_lab_container /bin/zsh
```

### 3. Verify Installation
```bash
# Check tools
subfinder -version
nuclei -version
nmap --version
```

---

## 🔍 Core Tools & Usage

### Subdomain Discovery

**SUBFINDER** - Fast subdomain enumeration
```bash
subfinder -d example.com -o subdomains.txt
```

**SUBLIST3R** - OSINT-based enumeration
```bash
sublist3r -d example.com -o results.txt
```

### Live Host Detection

**HTTPX** - HTTP probe & tech detection
```bash
cat subdomains.txt | httpx -o alive.txt
httpx -u https://example.com -tech-detect
```

### Vulnerability Scanning

**NUCLEI** - Template-based scanner
```bash
# Basic scan
nuclei -u https://example.com

# High severity only
nuclei -u https://example.com -severity high,critical

# Multiple targets
nuclei -l urls.txt -o vulnerabilities.txt
```

### Directory & File Discovery

**GOBUSTER** - Directory bruteforcer
```bash
gobuster dir -u https://example.com \
  -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt \
  -x php,html,js
```

**DIRSEARCH** - Advanced directory scanner
```bash
dirsearch -u https://example.com -e php,html,js
```

**FFUF** - Fast web fuzzer
```bash
ffuf -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt \
  -u https://example.com/FUZZ
```

### URL Collection

**GAU** - Get All URLs from archives
```bash
gau example.com > all_urls.txt
```

**WAYBACKURLS** - Wayback Machine URLs
```bash
waybackurls example.com | grep -E "admin|login|config"
```

### Port Scanning

**NAABU** - Fast port scanner
```bash
# Top 1000 ports
naabu -host example.com -top-ports 1000

# Scan multiple hosts
naabu -l hosts.txt -o ports.txt
```

**NMAP** - Network mapper
```bash
# Service detection
nmap -sV example.com

# Vulnerability scan
nmap --script vuln example.com
```

---

## ⚡ Practical Workflows

### Workflow 1: Complete Subdomain Analysis
```bash
# Discover subdomains
subfinder -d target.com -o subs.txt

# Filter live hosts
cat subs.txt | httpx -o alive.txt

# Scan for vulnerabilities
nuclei -l alive.txt -o vulns.txt
```

### Workflow 2: Web Application Testing
```bash
# Directory discovery
gobuster dir -u https://target.com \
  -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt

# Collect historical URLs
gau target.com > urls.txt

# Test for XSS vulnerabilities
nuclei -l urls.txt -t /root/nuclei-templates/vulnerabilities/xss/
```

### Workflow 3: Port & Service Analysis
```bash
# Fast port scan
naabu -host target.com -o ports.txt

# Service enumeration
nmap -sV target.com

# Check for known vulnerabilities
nmap --script vuln target.com
```

---

## 🛠️ Container Management

### Basic Operations
```bash
# View logs
docker logs vapt_lab_container

# Restart container
docker restart vapt_lab_container

# Stop lab
docker-compose down

# Rebuild
docker-compose down -v && docker-compose up --build -d
```

### Volume Location (WSL2)
```
\\wsl$\docker-desktop-data\data\docker\volumes\vapt_toolkit
```

---

## 🔧 Maintenance

### Update Tools
```bash
nuclei -update-templates
subfinder -up
```

### Fix Permissions
```bash
chmod +x /root/toolkit/*/
```

---

## ⚠️ Important Guidelines

1. **Authorization First** - Never test targets without explicit permission
2. **Use Legal Targets** - HackTheBox, TryHackMe, DVWA, PortSwigger Academy
3. **Document Everything** - Keep detailed notes of findings
4. **Chain Tools** - Combine tools for comprehensive assessments
5. **Stay Updated** - Regularly update tools and templates

---

## 🎯 Recommended Practice Platforms

- [HackTheBox](https://hackthebox.com) - Retired machines
- [TryHackMe](https://tryhackme.com) - Guided rooms
- [PortSwigger Academy](https://portswigger.net/web-security) - Free labs
- [VulnHub](https://vulnhub.com) - Vulnerable VMs
- [DVWA](https://github.com/digininja/DVWA) - Practice web app

---

## 📚 Additional Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [SecLists Wordlists](https://github.com/danielmiessler/SecLists)
- [Nuclei Templates](https://github.com/projectdiscovery/nuclei-templates)
- [Bug Bounty Methodology](https://github.com/jhaddix/tbhm)

---

## 💬 Support

For issues or questions:
- Open an issue on GitHub
- Check tool documentation
- Review Docker logs

---

**Remember:** Ethical hacking requires permission. Always test responsibly! 🔒