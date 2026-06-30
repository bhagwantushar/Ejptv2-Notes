
## SMB Enumeration

SMB is used for files and printer sharing on the networks. It mainly uses TCP 445, and older setup may also involve 139 via NETBIOS.
	Enumerating involves:
		- SMB version
		- shares
		- users
		- passwords through brute force in some cases

Why SMB matters:  
Because it can reveal a lot of useful information like shared folders, usernames, and possible authentication paths.

- SMB 1.0: The original version, which had security vulnerabilities. It was used with older
operating systems like Windows XP.
+ SMB 2.0/2.1: Introduced with Windows Vista/Windows Server 2008, offering improved
performance and security.
+ SMB 3.0+: Introduced with Windows 8/Windows Server 2012, adding features like
encryption, multichannel support, and improvements for virtualization.

# NetBIOS Enumeration

NetBIOS helps System to interact with each other on a local Network. These are the list of services:
- Name Service
- Datagram Service
- Session Service

Common ports:
- 137
- 138
- 139
Why it matters:  
NetBIOS can leak names, system details, and help you understand Windows network communication.

### Functions: NetBIOS offers three Primary Services:
- Name Service (NetBIOS-NS): Allows computers to register, unregister, and
resolve names in a local network.
+ Datagram Service (NetBIOS-DGM): Supports connectionless communication and
broadcasting.
+ Session Service (NetBIOS-SSN): Supports connection-oriented communication for
more reliable data transfers.

## NbtScan

nbtscan is a tool used to scan a network for NETBIOS Information and enumerate details for windows
It works by querying **NetBIOS Name Service (NBNS)** on **UDP port 137**.
- NetBIOS is used for **name resolution and communication in local networks**
- Uses ports **137, 138, 139**

## What information does nbtscan give?

When you run it, you can get:

- IP address
- NetBIOS name (computer name)
- Workgroup / domain name
- MAC address
- Device type (server/workstation)

### nbtscan Commands

## Basic Scan (MOST IMPORTANT)

1) nbtscan <IP-range>

### Example:

nbtscan 192.168.1.0/24

### What it does:

- Scans entire network
- Finds Windows machines
- Shows:
    - hostname
    - workgroup
    - IP

2) Scan Single Target
nbtscan <IP>

### Example:

nbtscan 192.168.1.10

3) Verbose Output (More Details)

nbtscan -v <IP-range>

### Example:

nbtscan -v 192.168.1.0/24

### What it does:

- Gives more detailed output
- Useful when normal scan is too limited

 4) Display MAC Address

nbtscan -m <IP-range>

### Example:

nbtscan -m 192.168.1.0/24

### Why useful?

- Helps identify:
    - device vendor
    - type of system

5.) Use Custom UDP Port (rare but good to know)

nbtscan -p <port> <IP>

👉 Default is **137**, so usually you don’t need this


---
# Core Concept (THIS IS THE ANSWER)

👉 There are **TWO ways to get access**:

### 1. Exploitation (no credentials)

- You break in using a vulnerability
- Example: EternalBlue (MS17-010)

👉 “I found a weakness → I forced my way in”

---

### 2. Authentication (using credentials)

- You log in using valid username/password or hash
- Example: `psexec.py`

👉 “I have the key → I just walk in”

psexec Tool

`psexec.py` is a tool from the Impacket suite used to:

execute commands on a remote Windows machine using valid credentials

# Simple Understanding

Think like this:

👉 You already have:

- username
- password (or NTLM hash)

Now you want:

> “Give me a shell on that Windows machine”

👉 That’s what `psexec.py` does.


SMB Enumeration

nmap -p445 --script smb-protocols <target-ip>
nmap -p445 --script smb-enum-users.nse <target-ip>
use hydra to brute force and get the password
psexec.py <user-name>@<target-ip>

or using msfconsole
search psexec
use windows/smb/psexec
set RHOSTS
set SMBUser 
set SMBPass
run

 