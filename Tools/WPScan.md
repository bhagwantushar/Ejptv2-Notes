WPScan

WPscan is wordpress vulnerability scanner  
You see a website → you suspect it's WordPress → WPScan helps you find:- Users 
- Plugins  
- Themes  
- Vulnerabilities  
- Login attack possibilities 


Basic Scan

wpscan --url http://target_ip
Here we will find WordPress-
- Version
- Theme
- Plugins


Enumerate Users

wpscan --url http://target_ip -e u
This gives usernames like:
- admin 
- john 
- etc.

Enumerate plugins

```
wpscan --url http://target/blog -e p
```
👉 Why?
Because plugins = easiest way to hack
Example:
- outdated plugin → exploit → shell 
---

🧩 Step 4: Vulnerability scan (optional API)

```
wpscan --url http://target/blog --api-token YOUR_TOKEN
```
👉 This tells:
- Known CVEs 
- Exploitable bugs 
---

🔥 Step 5: Password brute force

Now comes what you tried:
```
wpscan --url http://target/blog -U admin -P wordlist.txt
```

---

❌ Why your brute force FAILED

You said:

fasttrack.txt → no password found
This is NORMAL.

Reasons:

1724. Password not in that wordlist 
1725. CTF expects another path (not brute force) 
1726. Username might be wrong 
1727. Login form might be protected 
---

🧠 IMPORTANT: Don't brute force blindly

👉 In CTFs, brute force is last step, not first.
---

🧩 What you SHOULD do next (based on your situation)

You found:
- /blog/wp-login.php
- admin user 
- no password from WPScan 
👉 Now think like hacker:
---

🔍 Check for:


1. Hidden files

```
gobuster dir -u http://target/blog -w wordlist.txt
```
Look for:
- backups 
- config files 
- uploads 
---

2. RSS feed (VERY IMPORTANT — YOU FOUND THIS)

You downloaded a feed file earlier 👇
👉 That is GOLD 💰
Open it and check:
- usernames 
- comments 
- hidden info 
- passwords (sometimes inside!) 
---

3. Try default credentials

Before brute force:
- admin:admin 
- admin:password 
- admin:123456 
---

4. Look for vulnerable plugins

If WPScan shows plugin like:
- revslider 
- file upload plugin 
👉 exploit instead of brute force
---

5. Try XML-RPC attack (advanced)

Sometimes login brute force works better via:
```
/xmlrpc.php
```

---

💡 Real hacker mindset (IMPORTANT)

Right now you're doing:
❌ "I got admin → brute force → stuck"
Instead do:
✅ "What other attack surface exists?"
---

🧭 For YOUR current CTF (very likely path)

Based on your screenshots:
👉 HIGH chance solution is:
- RSS feed leak 
- Hidden file in /wp-content/
- Plugin vulnerability 
NOT brute force
---

🧠 Summary (remember this)

WPScan is used to:
Step
Purpose
-e u
Find users
-e p
Find plugins
scan
detect version
brute force
LAST option

---

🚀 Now your task (important)

Do this and tell me results:
3460. Run: 
```
wpscan --url http://target/blog -e u,p
```
2. Open that feed file you downloaded
3. Tell me: 
- What users you see 
- Any weird text/password-like strings 
---
Then I’ll guide you like real pentester 🔥


