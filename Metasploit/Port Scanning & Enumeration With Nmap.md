
#### Nmap (Network Mapper)

Nmap is used to discover hosts and scan targets for open ports and services

Used to:
- Discover **live hosts**
- Find **open ports**
- Identify **services**
- Detect **OS**

### Host Discovery
Before Attacking, you need to know 
which machine exist in the network
## Command

nmap -sn 192.168.1.0/24
###  Meaning:
- `-sn` = Ping scan (no port scan)
- Only checks **alive hosts**
- -oX = Output scan in Normal 

## Importing Nmap Scan Results Into MSF

Nmap results can be imported into MSF for vulnerability detection and exploitation

Think like attacker:
Nmap = finds targets  
MSF (Metasploit) = exploits targets

Instead of manually typing everything again, we:
- Scan with Nmap  
-  Import into MSF  
-  Use it for exploitation

# Step-by-Step Process

## Step 1: Run Nmap and save output

nmap -sV -oX scan.xml 192.168.1.10

### Important:

- `-oX` = output in **XML format**  
    MSF understands XML (not normal text)

---

## Why XML?

Because:
- Structured data
- Easy for tools to parse
## Step 2: Start Metasploit

msfconsole

---
## Step 3: Import the scan

db_import scan.xml

## Step 4: Check Imported Data

## Show hosts
hosts

## Show services
services

nmap -sV -Pn -oX result_scan.xml <target-ip>
db_status
db_import result_scan.xml
hosts
services

