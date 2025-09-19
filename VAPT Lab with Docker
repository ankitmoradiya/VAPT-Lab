# VAPT Lab Workshop - Commands & Demonstrations

## 🚀 Initial Setup Commands

### 1. Build and Start the Lab
```bash
# Build and start the container
docker-compose up --build -d

# Alternative: Start without rebuild
docker-compose up -d

# Check if container is running
docker ps
```

### 2. Access the Lab Environment
```bash
# Enter the VAPT lab container
docker exec -it vapt_lab_container /bin/zsh

# Show available tools
show-tools
```

### 3. Docker Volume Management
```bash
# List docker volumes
docker volume ls

# Inspect volume location
docker volume inspect vapt_toolkit

# Windows WSL2 Volume Location:
\\wsl$\docker-desktop-data\data\docker\volumes\
```

---

## 🛠️ Tool Demonstrations

### 1. SUBFINDER - Subdomain Discovery
```bash
# Basic subdomain enumeration
subfinder -d example.com

# Save results to file
subfinder -d example.com -o subdomains.txt

# Use multiple sources
subfinder -d example.com -all
```

### 2. HTTPX - HTTP Toolkit
```bash
# Check if subdomains are alive
cat subdomains.txt | httpx

# Get HTTP status codes and titles
cat subdomains.txt | httpx -status-code -title

# Check for specific technologies
echo "example.com" | httpx -tech-detect
```

### 3. NUCLEI - Vulnerability Scanner
```bash
# Basic vulnerability scan
nuclei -u https://example.com

# Scan multiple targets
nuclei -l subdomains.txt

# Use specific templates
nuclei -u https://example.com -t /root/nuclei-templates/cves/

# High severity only
nuclei -u https://example.com -severity high,critical
```

### 4. GOBUSTER - Directory/File Bruteforcer
```bash
# Directory brute force
gobuster dir -u https://example.com -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt

# With specific extensions
gobuster dir -u https://example.com -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt -x php,html,js

# DNS subdomain brute force
gobuster dns -d example.com -w /root/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

### 5. FFUF - Web Fuzzer
```bash
# Directory fuzzing
ffuf -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt -u https://example.com/FUZZ

# Parameter fuzzing
ffuf -w /root/wordlists/SecLists/Discovery/Web-Content/burp-parameter-names.txt -u https://example.com/?FUZZ=test

# Virtual host fuzzing
ffuf -w /root/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u https://example.com -H "Host: FUZZ.example.com"
```

### 6. SUBLIST3R - Subdomain Enumeration
```bash
# Basic enumeration
sublist3r -d example.com

# Save results and enable brute force
sublist3r -d example.com -o sublist3r_results.txt -b

# Specify threads for faster scanning
sublist3r -d example.com -t 20
```

### 7. NAABU - Port Scanner
```bash
# Basic port scan
naabu -host example.com

# Scan specific ports
naabu -host example.com -p 21,22,25,53,80,110,143,443,993,995

# Scan top 1000 ports
naabu -host example.com -top-ports 1000

# Scan multiple hosts
naabu -l subdomains.txt
```

### 8. GAU - Get All URLs
```bash
# Fetch URLs from various sources
gau example.com

# Filter specific file extensions
gau example.com | grep -E "\.(js|php|json)$"

# Save all URLs
gau example.com > all_urls.txt
```

### 9. WAYBACKURLS - Wayback Machine URLs
```bash
# Get URLs from Wayback Machine
waybackurls example.com

# Filter for specific paths
waybackurls example.com | grep -E "admin|login|panel"

# Combine with other tools
waybackurls example.com | httpx | nuclei
```

### 10. DIRSEARCH - Directory Discovery
```bash
# Basic directory search
dirsearch -u https://example.com

# With custom wordlist
dirsearch -u https://example.com -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt

# Multiple extensions
dirsearch -u https://example.com -e php,html,js,txt

# Recursive search
dirsearch -u https://example.com -r
```

### NMAP - Network Scanning (Bonus)
```bash
# Basic host discovery
nmap -sn 192.168.1.0/24

# Port scan with service detection
nmap -sV example.com

# Vulnerability scan
nmap --script vuln example.com

# Fast scan
nmap -F example.com
```

---

## 🔗 Tool Chaining Examples

### Example 1: Complete Subdomain Analysis
```bash
# Step 1: Find subdomains
subfinder -d example.com -o subs.txt

# Step 2: Check which are alive
cat subs.txt | httpx -o alive_subs.txt

# Step 3: Scan for vulnerabilities
nuclei -l alive_subs.txt -o vulnerabilities.txt
```

### Example 2: Web Application Testing
```bash
# Step 1: Directory discovery
gobuster dir -u https://target.com -w /root/wordlists/SecLists/Discovery/Web-Content/common.txt -o dirs.txt

# Step 2: Get all URLs
gau target.com > all_urls.txt

# Step 3: Test for XSS/Injection
nuclei -l all_urls.txt -t /root/nuclei-templates/vulnerabilities/xss/ -o xss_results.txt
```

### Example 3: Port and Service Analysis
```bash
# Step 1: Port scan
naabu -host target.com -o open_ports.txt

# Step 2: Service enumeration
nmap -sV -iL <(cut -d: -f1 open_ports.txt | sort -u)

# Step 3: Vulnerability assessment
nmap --script vuln target.com
```

## 🔧 Troubleshooting Commands

### Container Management
```bash
# View container logs
docker logs vapt_lab_container

# Restart container
docker restart vapt_lab_container

# Stop and remove
docker-compose down

# Rebuild from scratch
docker-compose down -v
docker-compose up --build -d
```

### Common Issues
```bash
# Fix permission issues
chmod +x /root/toolkit/*/

# Update tool databases
nuclei -update-templates
subfinder -up

# Check tool versions
nuclei -version
subfinder -version
```

---

## 📝 Notes for Students

1. **Always get proper authorization** before testing any target
2. **Use test environments** like HackTheBox, TryHackMe, or DVWA
3. **Practice tool chaining** for comprehensive assessments  
4. **Document your findings** systematically
5. **Keep tools updated** regularly for latest capabilities

## 🎯 Recommended Practice Targets

- **DVWA** (Damn Vulnerable Web Application)
- **VulnHub VMs**
- **HackTheBox Retired Machines**
- **TryHackMe Rooms**
- **PortSwigger Web Security Academy**
