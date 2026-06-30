### Port Scanning

Port scanning is the process of identifying:

- Open ports on a target system
- Services running on those ports
- Service versions (sometimes)

👉 Example:

- Port 22 → SSH
- Port 80 → HTTP
- Port 445 → SMB

### 🔹 Enumeration

Enumeration goes deeper:

- Identifies usernames, shares, system info
- Finds service versions and configurations
- Helps identify vulnerabilities for exploitation

👉 Example:  
If port 445 (SMB) is open:
- You enumerate SMB shares
- Check for anonymous access
- Find vulnerable services

# What is Armitage?
Armitage is a **graphical cyber attack management tool** for the Metasploit Framework. It provides a visual interface to:
- A **GUI for Metasploit**
- Helps visualize targets and exploits
- Automates scanning and exploitation workflows

Instead of typing MSF commands, you:  
👉 click, scan, and analyze visually


# Basic Workflow in Armitage

### Step 1: Start Metasploit + Armitage

In Kali Linux:

```
sudo service postgresql startsudo msfdb initarmitage
```

Connect to Metasploit when prompted.

## Lab 

service postgresql start && msfconsole 
in a new tab - armitage
hosts -> add hosts
right click on the target computer and scan
attacks nmap->OS discovery

---

# 🧪 Armitage Lab: Exploitation & Post-Exploitation (Explained Simply)

This lab shows how a vulnerability in a service (Rejetto HTTP File Server) is used to gain access to a system and then extract useful information using Meterpreter.

---

# 🟢 STEP 1: Open Lab Environment

You start by:

- Launching the **Kali Linux GUI instance**
    
- Opening Armitage inside Kali
    

👉 Purpose:  
You are working in a **controlled penetration testing environment (lab)**, not a real network.

---

# 🔍 STEP 2: Port Scanning & Enumeration (Already Done in Previous Lab)

Before exploitation, you already discovered:

- Target system: `demo1.ine.local`
    
- Open port: **80 (HTTP)**
    
- Service: **Rejetto HTTP File Server**
    

📌 Why this matters:

- Port 80 = web service
    
- Rejetto HTTP File Server is known to have vulnerabilities
    
- So it becomes an **attack entry point**
    

---

# ⚠️ STEP 3: Identify Exploit Module in Armitage

In Armitage:

### What you do:

- Search for “Rejetto” or service name in module panel
    
- Select exploit module
    

📌 What Armitage does:

- Matches service → known Metasploit exploit
    

👉 Example:

- Service detected → Rejetto HTTP File Server
    
- Exploit suggested → Remote code execution module
    

---

# ⚙️ STEP 4: Configure Exploit (RHOSTS)

You are asked to set:

### RHOSTS = `demo1.ine.local`

📌 Meaning:

- RHOSTS = **Remote Host**
    
- This tells the tool:  
    👉 “Attack this target machine”
    

Then you click:  
✔ **Launch**

---

# 💥 STEP 5: Exploitation (Getting Access)

When exploit runs successfully:

✔ Vulnerability is triggered  
✔ Payload is delivered  
✔ Reverse connection is created

👉 Result:  
You get a **Meterpreter session**

---

# 🧠 What is Meterpreter?

Meterpreter is:

- A powerful remote control shell
    
- Runs inside memory (hard to detect)
    
- Used after exploitation
    

👉 Think of it as:

> “Full remote control interface of the victim system”

---

# 🟡 STEP 6: Session Interaction

You now right-click the target:

> Meterpreter 1 → Interact → Meterpreter Shell

📌 This opens a command interface to control the system.

---

# 🖥️ STEP 7: System Information Gathering

You run:

```bash
sysinfo
```

### What it gives:

- Operating system
    
- Computer name
    
- Architecture
    
- System details
    

### Example output:

- Windows 7 / Windows Server
    
- Hostname of machine
    
- x86 or x64 system
    

📌 Why this is important:  
Helps attacker understand:

- System type
    
- Next possible exploits (privilege escalation)
    

---

# 🔐 STEP 8: Dumping Password Hashes

You right-click target:

> Meterpreter 1 → Dump Hashes

### What happens:

- Windows password hashes are extracted
    

These hashes include:

- Username
    
- NTLM hash values
    

Example format:

```
Administrator:500:hash:hash
User:1000:hash:hash
```

---

# 🧠 Why hash dumping is important

- Passwords are not shown directly
    
- Instead, encrypted versions (hashes) are extracted
    
- These can be used for:
    
    - cracking passwords
        
    - lateral movement (Pass-the-Hash attacks)
        

---

# 🔴 STEP 9: Post-Exploitation Summary

After gaining access, attacker can:

### ✔ System Info

- `sysinfo`
    

### ✔ User Data

- account hashes
    

### ✔ Further actions (not shown but possible):

- Screenshot capture
    
- Keylogging
    
- File download/upload
    
- Persistence setup
    

---

# 🧾 FINAL FLOW (VERY IMPORTANT FOR NOTES)

```
1. Scan target → find open port 80
2. Identify service → Rejetto HTTP File Server
3. Search exploit in Armitage
4. Set RHOSTS = demo1.ine.local
5. Launch exploit
6. Get Meterpreter session
7. Run sysinfo
8. Dump password hashes
```

---

# 🎯 KEY EXAM POINTS

### Exploitation phase:

- Identify vulnerable service
    
- Select matching exploit module
    
- Configure RHOSTS
    
- Launch attack
    
- Gain Meterpreter access
    

### Post-exploitation phase:

- System reconnaissance (`sysinfo`)
    
- Credential extraction (hash dumping)
    
- Prepare for further attack steps
    

---

# 💡 Simple Understanding

Think of it like:

- 🧭 Scan → find unlocked door (port 80)
    
- 🔓 Exploit → break door lock (Rejetto vulnerability)
    
- 🏠 Access → enter system (Meterpreter)
    
- 🔍 Explore → check system info + steal credentials
    

---

If you want, I can turn this into:  
✔ 1-page revision sheet  
✔ CEH exam questions from this lab  
✔ Or a diagram of the full attack flow (very useful for exams)