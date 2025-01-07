| **Tool/Category** | **Purpose** | **Command Examples** | **Notes** |
| --- | --- | --- | --- |
| **Nmap Basics** |  |  |  |
| TCP Connect Scan | Basic scan for open TCP ports. | `nmap -sT <target>` | Slower than SYN scan but doesn’t require root privileges. |
| SYN Scan | Faster and stealthier TCP port scan. | `nmap -sS <target>` | Requires root privileges. |
| Service and Version Detection | Detect running services and versions. | `nmap -sV <target>` | Combines with other flags for deeper enumeration. |
| OS Detection | Detect operating system and device type. | `nmap -O <target>` | Use when you suspect vulnerable services tied to specific OS versions. |
| Scan and Save Output | Save results in all formats (normal, grepable, and XML). | `nmap -oA <output_file> <target>` | Essential for documentation and reporting. |
| **Nmap NSE Scripts** |  |  |  |
| Default Script Scan | Run default NSE scripts for common vulnerabilities and service info. | `nmap -sC <target>` | Includes scripts like `http-title`, `smb-os-discovery`, and more. |
| SMB Enumeration | Enumerate SMB shares, users, and OS information. | `nmap --script smb-enum-shares,smb-enum-users,smb-os-discovery -p 445 <target>` | Useful for enumerating SMB services. |
| HTTP Vulnerabilities | Check for common HTTP vulnerabilities. | `nmap --script http-vuln* -p 80,443 <target>` | Replace `http-vuln*` with specific scripts like `http-vuln-cve2017-5638`. |
| Brute Force Enumeration | Perform brute force attacks using scripts. | `nmap --script ssh-brute -p 22 <target>` | Replace `ssh-brute` with other brute-force scripts like `ftp-brute` or `smtp-enum-users`. |
| **Advanced Nmap Usage** |  |  |  |
| Exclude Hosts | Exclude specific hosts from scans. | `nmap <targets> --exclude <host1>,<host2>` | Helps refine scans and avoid unnecessary traffic to known safe hosts. |
| Specific Port Range | Scan specific ports. | `nmap -p 1-1000 <target>` | Replace `1-1000` with desired range or comma-separated ports (e.g., `22,80,443`). |
| UDP Scanning | Scan for open UDP ports. | `nmap -sU -p 53,123 <target>` | Slower and often less reliable than TCP scans. |
| Aggressive Mode | Combine OS detection, service detection, and default scripts. | `nmap -A <target>` | Useful for a detailed overview but noisier. |
| **Other Port Enumeration Tools** |  |  |  |
| **Masscan** | High-speed port scanning. | `masscan -p1-65535 --rate=1000 -oG masscan_results <target>` | Ideal for scanning large networks quickly. |
| **RustScan** | Fast port scanner that integrates with Nmap. | `rustscan -a  --ulimit 5000 | nmap -sC -sV -p- ` |
| **Service-Specific Enumeration** |  |  |  |
| SMB Enumeration | Enumerate shares and users. | `smbclient -L //<target>`  `enum4linux -a <target>` | Useful for SMB reconnaissance on port 445. |
| HTTP Enumeration | Discover directories and files. | `gobuster dir -u http://<target> -w /path/to/wordlist.txt` | Replace `gobuster` with `ffuf` or `dirb` if preferred. |
| FTP Enumeration | Check for anonymous login and list files. | `ftp <target>`  `nmap --script ftp-anon -p 21 <target>` | Identifies misconfigured FTP servers. |
| DNS Enumeration | Enumerate DNS records and perform zone transfers. | `dnsenum <domain>`  `dig axfr @<nameserver> <domain>` | Zone transfers (`dig`) may expose additional subdomains and services. |
| SNMP Enumeration | Query SNMP services for public information. | `onesixtyone -c community_strings.txt <target>`  `snmpwalk -v2c -c <community_string> <target>` | SNMP often exposes device info, running services, and configurations. |
| **Initial Vulnerability Scans** |  |  |  |
| Nikto | Scan web servers for known vulnerabilities. | `nikto -h http://<target>` | Combines well with directory enumeration. |
| WhatWeb | Identify technologies and versions of web servers and applications. | `whatweb http://<target>` | Helps to identify possible version-specific vulnerabilities. |
| SSL Scanning | Scan for SSL/TLS vulnerabilities. | `sslscan <target>` | Useful for identifying weak SSL/TLS configurations and cipher suites. |
   
