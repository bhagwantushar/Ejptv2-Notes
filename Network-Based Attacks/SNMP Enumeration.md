SNMP Stands for Simple Network Management Protocol. It is a widely used protocol for **monitoring and managing networked devices** such as routers, switches, printers, and servers. It lets administrators query devices for status information, configure certain settings, and receive alerts called traps.

In penetration testing, SNMP can be very useful because it may expose a lot of information about the target device. The PDF says SNMP enumeration helps gather information that can reveal **vulnerabilities, misconfigurations, or points of attack**.

The PDF explains SNMP using 3 main parts:

**1. SNMP Manager**  
The system that sends queries to SNMP-enabled devices.

**2. SNMP Agent**  
The software running on the device that answers those queries and can also send traps.

**3. MIB (Management Information Base)**  
A hierarchical database that defines the structure of the available SNMP data. Each item has a unique **OID** (Object Identifier).

## Versions

The PDF mentions 3 versions:

**SNMPv1**  
Oldest version. Uses **community strings** for authentication.  
Think of a community string like a simple password.

**SNMPv2c**  
Improved version with support for bulk transfers, but still relies on community strings.

**SNMPv3**  
Adds better security, including **encryption, message integrity, and user-based authentication**.

## Ports

The PDF says:

- **UDP 161** → used for SNMP queries
- **UDP 162** → used for SNMP traps/notifications

```
nmap -sU -p 161 --script=snmp-brute demo.ine.local
```

# SNMPWalk

**`snmpwalk`** is a tool used to **query SNMP-enabled devices and retrieve information from their MIB (Management Information Base)**.

Think like this:

- SNMP device = 📚 library
- MIB = 📖 catalog of all data
- OID = 📌 index number for each item

👉 `snmpwalk` =  
You walk through the entire library and read all entries one by one.