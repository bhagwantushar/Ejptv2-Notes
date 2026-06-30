Network Enumeration is the phase that comes after host discovery and port scanning.
The goal is to collect more detailed information about the target hosts and the services running on them, such as account names ,shares and misconfigurations. It is an active phase as it makes connections with the target systems.

## Why it matters

Port scanning only tells you things like:

- host is alive
- port 22 is open
- port 445 is open

Enumeration goes one step further and answers:

- what exact service is running there?
- which version is it?
- are there users, shares, weak configs, or useful data?
- can this service become an attack path later?
**Information Gathering → Host Discovery → Port Scanning → Service Detection / OS Detection → Enumeration → Exploitation**.

So remember this:

**scan first, enumerate next, exploit later**

## What you usually enumerate

common network/service enumeration includes:

- FTP
- SMB
- Web servers / HTTP
- MySQL
- SSH
- SMTP
- NetBIOS
- SNMP