Networking Fundamentals and the OSI Model

Successful network mapping and security assessments require a deep understanding of how data moves across systems.

The OSI Model

The Open Systems Interconnection (OSI) model standardizes computing functions into seven abstraction layers to ensure interoperability.

Layer	Name	Function	Examples
7	Application	Network services for users/apps	HTTP, FTP, DNS, SSH
6	Presentation	Data translation, encryption, compression	SSL/TLS, JPEG, GIF
5	Session	Interhost communication management	APIs, NetBIOS, RPC
4	Transport	End-to-end communication, flow control	TCP, UDP
3	Network	Logical addressing and routing	IP, ICMP, IPSec
2	Data Link	Physical addressing (MAC), error detection	Ethernet, Switches, PPP
1	Physical	Physical connection between devices	Fiber, Hubs, USB, Cables

Transport Layer Protocols: TCP vs. UDP

* Transmission Control Protocol (TCP): A connection-oriented, reliable protocol. It uses a Three-Way Handshake (SYN -> SYN-ACK -> ACK) to establish a connection before data exchange. It ensures ordered delivery and supports retransmission of lost packets.
* User Datagram Protocol (UDP): A connectionless, faster protocol focusing on efficiency. It is "unreliable" as it provides no guarantees for delivery or ordering, making it ideal for real-time applications like VOIP and streaming.

Internet Protocol (IP) and ICMP

* IPv4 vs. IPv6: IPv4 utilizes 32-bit addresses (e.g., 192.168.0.1), while IPv6 uses 128-bit hexadecimal addresses to solve address exhaustion.
* ICMP (Internet Control Message Protocol): Used for diagnostics and error reporting. The ping utility relies on ICMP Echo Requests (Type 8, Code 0) and Echo Replies (Type 0, Code 0).


--------------------------------------------------------------------------------


2. Information Gathering and Reconnaissance

Information gathering is the initial phase of penetration testing, divided into passive and active methodologies.

Passive Information Gathering (OSINT)

Passive reconnaissance involves collecting data without direct interaction with the target.

* Whois Enumeration: Collecting registration details (owner, email, DNS servers, IP blocks).
* Google Dorks: Advanced search queries (e.g., site:, filetype:, intitle:) to find exposed sensitive information or subdomains.
* theHarvester: An OSINT tool that gathers emails, subdomains, and hostnames from public sources like Google and Bing.
* Netcraft: Used for website footprinting to identify hosting providers, server technology, and OS info.

Active Information Gathering: Host Discovery

This phase involves interacting with the network to identify live hosts and open ports.

* Ping Sweeps: Sending ICMP Echo Requests to a range of IP addresses. While quick, they are easily detected and often blocked by firewalls.
* ARP Scanning: Effective for local networks within the same broadcast domain.
* TCP SYN Ping: A "half-open" scan that is stealthier than ICMP; a SYN-ACK response indicates a live host.
* UDP Ping: Useful for discovering hosts that block ICMP or TCP probes.

Scanning with Nmap

Nmap (Network Mapper) is the industry standard for network discovery and security auditing.

* Common Scan Types:
  * -sS (SYN Scan): Stealthy, does not complete the 3-way handshake.
  * -sT (TCP Connect Scan): Completes the connection; usually logged by applications.
  * -sU (UDP Scan): Used to find open UDP ports.
  * -sV: Service version detection.
  * -O: Operating system fingerprinting.
* Timing Templates: Ranges from -T0 (Paranoid/Slow) to -T5 (Insane/Fast), allowing testers to optimize for stealth or speed.


--------------------------------------------------------------------------------


3. Vulnerability Analysis and Exploitation

Once a target's surface is mapped, testers look for vulnerabilities to gain unauthorized access.

Buffer Overflow Vulnerabilities

A buffer overflow occurs when data exceeds a buffer's storage capacity, overflowing into adjacent memory and corrupting data.

* Stack-based: The most common type; involves overwriting the return pointer on the execution stack to hijack the program's path.
* Heap-based: Flooding memory used for dynamic runtime operations; more complex to exploit.
* Prevention Mechanisms:
  * ASLR (Address Space Layout Randomization): Randomizes memory addresses to make code location unpredictable.
  * DEP (Data Execution Prevention): Marks memory regions as non-executable to prevent malicious code runs.
  * SEHOP: Protects against overwriting the Structured Exception Handling (SEH) chain.

Web Application Testing with Burp Suite

Burp Suite is an HTTP interception proxy that allows testers to modify requests between the browser and the server.

* Proxy: Intercepts and modifies web traffic.
* Intruder: Automates customized attacks (brute forcing, fuzzing).
* Repeater: Manually modifies and resends individual HTTP requests to analyze responses.
* Decoder/Comparer: Tools for transforming data (encoding/hashing) and finding differences between responses.

Common Web Vulnerabilities

* SQL Injection (SQLi): Manipulating database queries via user input (e.g., ' OR 'a'='a).
* Cross-Site Scripting (XSS): Injecting malicious scripts into web pages viewed by other users.
* Misconfigured HTTP Methods: Exploiting the PUT method to upload malicious shells to a server.


--------------------------------------------------------------------------------


4. Privilege Escalation and Defensive Mitigation

Privilege escalation is the process of increasing access rights beyond initial grants.

Types of Privilege Escalation

* Vertical: Gaining higher-level permissions (e.g., standard user to Administrator/Root).
* Horizontal: Gaining the credentials of another user with similar privilege levels.

Techniques Used by Attackers

* Exploiting Software Vulnerabilities: Leveraging flaws like buffer overflows or remote code execution.
* Misconfigured Permissions: Manipulating weak access controls or improper file permissions.
* Social Engineering: Tricking users into revealing credentials (phishing).
* Lateral Movement: Using a compromised system as a "stepping stone" to move through the network.

Endpoint Privilege Management (EPM) Strategies

EPM solutions like Admin By Request aim to enforce the "Principle of Least Privilege."

* Privilege Elevation: Prompting for credentials only when necessary for specific tasks.
* Application Control: Restricting unauthorized software execution.
* Network Segmentation: Dividing networks into smaller segments to prevent lateral movement.
* MFA (Multi-Factor Authentication): Adding layers of security beyond simple passwords.


--------------------------------------------------------------------------------


5. Post-Exploitation: Pivoting and Tunneling

Pivoting allows a tester to use a compromised host to access unreachable parts of a network.

SSH Tunneling and Port Forwarding

* Local Port Forwarding (-L): Forwards a port from the client machine to the server machine.
* Remote Port Forwarding (-R): Forwards a port from the server machine back to the client.
* SOCKS Proxy (-D): Turns the SSH connection into a proxy, allowing tools like Firefox or Nmap (via proxychains) to route traffic through the compromised host.

Meterpreter for Pivoting

In the Metasploit Framework, the Meterpreter shell provides built-in pivoting capabilities:

* autoroute: Automatically adds routes to subnets reachable by the compromised host.
* portfwd: Forwards specific ports to the local machine for further scanning or exploitation.


--------------------------------------------------------------------------------


6. Professional Certification: The eJPT

The Junior Penetration Tester (eJPT) certification validates foundational knowledge in red teaming and penetration testing.

Exam Domains and Objectives

* Assessment Methodologies (25%): Identifying hosts, ports, services, and OS types.
* Host and Network Auditing (25%): Enumerating users, system info, and transferring files.
* Host and Network Penetration Testing (35%): Exploitation with Metasploit, pivoting, and brute-forcing.
* Web Application Penetration Testing (15%): Vulnerability identification and reconnaissance.

Critical Exam Success Factors

* Enumeration: Sources emphasize that "mastering enumeration is the real secret to passing."
* Pivoting: Practical knowledge of adding routes and port forwarding is essential for reaching isolated network segments.
* Documentation: Candidates are encouraged to maintain detailed personal notes, as many exam answers are derivable from well-organized course materials.
