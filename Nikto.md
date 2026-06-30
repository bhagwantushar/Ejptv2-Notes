Nikto is a classic **web server vulnerability scanner** used in penetration testing. It checks for dangerous files, misconfigurations, outdated software, and known vulnerabilities on web servers.

Below is a **clear, practical guide to Nikto commands with examples** so you can actually use it in labs or CTFs.

---

# 🔧 1. Basic Nikto Command Structure

```bash
nikto -h <target>
```

### Example:

```bash
nikto -h http://192.168.1.10
```

👉 This scans the web server running on that IP (port 80 by default).

---

# 🌐 2. Scanning a Domain

```bash
nikto -h http://example.com
```

### Example:

```bash
nikto -h http://testphp.vulnweb.com
```

👉 Scans a live website for vulnerabilities.

---

# 🚪 3. Scanning a Specific Port

If the web server is running on a non-standard port:

```bash
nikto -h http://target.com -p <port>
```

### Example:

```bash
nikto -h http://192.168.1.10 -p 8080
```

👉 Scans HTTP service on port 8080.

---

# 🔐 4. HTTPS Scanning

```bash
nikto -h https://target.com
```

### Example:

```bash
nikto -h https://testsite.com
```

👉 Important for SSL/TLS-enabled websites.

---

# 📁 5. Save Output to a File

### HTML report:

```bash
nikto -h http://target.com -o report.html -Format html
```

### Text report:

```bash
nikto -h http://target.com -o report.txt -Format txt
```

### CSV report:

```bash
nikto -h http://target.com -o report.csv -Format csv
```

---

# ⚡ 6. Fast Scan Mode

```bash
nikto -h http://target.com -Tuning 4
```

👉 Tuning controls scan type.

### Common tuning values:

|Value|Meaning|
|---|---|
|1|Interesting files|
|2|Misconfigurations|
|3|Information disclosure|
|4|Injection issues|
|5|Remote file retrieval|

### Example:

```bash
nikto -h http://target.com -Tuning 1,2,3
```

---

# 🧪 7. Use a Proxy (Burp Suite)

```bash
nikto -h http://target.com -useproxy http://127.0.0.1:8080
```

👉 Sends traffic through Burp Suite for interception.

---

# 🧭 8. Specify a User Agent

```bash
nikto -h http://target.com -useragent "Mozilla/5.0"
```

👉 Useful to avoid blocking or mimic browsers.

---

# ⏱ 9. Increase Timeout

```bash
nikto -h http://target.com -timeout 10
```

👉 Useful for slow servers.

---

# 🧾 10. Display Verbose Output

```bash
nikto -h http://target.com -Display V
```

### Options:

- `V` → verbose
    
- `D` → debug
    
- `E` → errors
    
- `P` → progress
    

---

# 🔄 11. Update Nikto Database

```bash
nikto -update
```

👉 Keeps vulnerability signatures up to date.

---

# 🧠 12. Scan Multiple Targets

```bash
nikto -h targets.txt
```

### Example file:

```
http://192.168.1.10
http://192.168.1.11
http://testsite.com
```

---

# 🧪 13. Realistic Pentesting Example

```bash
nikto -h http://192.168.56.101 -p 80 -Tuning 1,2,3 -o scan.html -Format html
```

👉 This:

- scans target IP
    
- checks key vulnerabilities
    
- saves report in HTML
    

---

# 📊 What Nikto Actually Finds

Typical results include:

- ❌ Outdated Apache/Nginx versions
    
- ❌ Dangerous files (like `/admin/`, `/backup.zip`)
    
- ❌ Directory listing enabled
    
- ❌ HTTP headers missing (security headers)
    
- ❌ Default files (phpinfo, test pages)
    

---

# ⚠️ Important Real-World Note

Nikto is:

- ✔️ Fast for reconnaissance
    
- ✔️ Great for beginners and CTFs
    
- ❌ Noisy (easily detected by IDS/IPS)
    
- ❌ Not stealthy (don’t rely on it alone)
    

---

# 🚀 If you want next step

I can teach you:

- Nikto vs Nmap vs WhatWeb (when to use each)
    
- How to combine Nikto with Burp Suite workflow
    
- Real CTF walkthrough using Nikto
    
- How to interpret Nikto results like a pentester
    

Just tell me 👍


Basic usage beginner

nikto -h <target>

Scan a host. Target can be an IP address, hostname, or full URL.  
nikto -h 192.168.1.10

nikto -h <target> -p <port>

Scan a specific port. Default is 80; use 443 for HTTPS.  
nikto -h 192.168.1.10 -p 8080

nikto -h <target> -ssl

Force SSL/HTTPS scan. Use when the target runs on HTTPS.  
nikto -h https://example.com -ssl

nikto -h <target> -o report.txt

Save results to a file. Supports formats: txt, csv, html, xml, nbe.  
nikto -h 10.0.0.1 -o out.html -Format html