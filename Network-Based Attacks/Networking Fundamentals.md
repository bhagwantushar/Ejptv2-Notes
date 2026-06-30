Network Fundamentals are the basic concepts of how computers communicate over each other over a network.

Communication happens using:

- Protocols
- Packets
- Layers(OSI Model)

#### Network Protocols

Protocols are the rules that allows computers to communicate
Example -
Like how humans use English, Computers uses Protocols

###### Common Protocols

| Protocol | Purpose              |
| -------- | -------------------- |
| HTTP     | Web Communication    |
| FTP      | File Transfer        |
| SSH      | Remote Login         |
| DNS      | Convert Domain -> IP |
| SMB      | File sharing         |

##### Packets
A Packet is a small unit of data sent over a network, Data is transferred using packets.

##### Structure of a Packet
Every Packet has:
1) Header
	 - Info about:
		 - Source IP
		 - Destination IP
		 - Protocol
2) Payload
	- Actual Data(files,message,etc)
### Why Hacker Cares
Because:
- You analyze packets → sniff traffic
- You manipulate packets → attacks

# OSI(Open System Interconnection) Model

OSI Model is a conceptual framework that standardizes the functions of a telecommunication or computing system into seven abstraction layers.

| Layer | Name         | What it does       | Example  |
| ----- | ------------ | ------------------ | -------- |
| 7     | Application  | User interaction   | HTTP     |
| 6     | Presentation | Format, encryption | SSL/TLS  |
| 5     | Session      | Manage sessions    | APIs     |
| 4     | Transport    | Data delivery      | TCP/UDP  |
| 3     | Network      | IP addressing      | IP       |
| 2     | Data Link    | MAC + switching    | Ethernet |
| 1     | Physical     | Cables/signals     | Wi-Fi    |
### Easy Way to Remember

“**All People Seem To Need Data Processing**”

(Application → Physical)

1) Layer 1 - Physical layer
	Deals with Physical Connections between Devices.
	Example - Cables,USB,Ethernet Cables

2) Layer 2 - Data Link
   Sending Data Between Devices on the same local Network (LAN)
   It handles **framing, MAC addressing, and error detection**
   This layer adds:
	 - Source MAC
	 - Destination MAC
   This is used for **local delivery**
   Frame = Packet + MAC info
### MAC Addressing 
A Unique Physical Address Assigned to a device's network Card(NIC)
- It identifies a device inside the local network (LAN)
- Works at layer 2(Data link Layer)
Example:
00:1A:2B:3C:4D:5E
- 6 pairs of hexadecimal numbers
- Assigned by manufacturer

### Easy Way to Understand

IP = “Where are you?”  
MAC = “Who are you?

### Framing 
Breaks the data into frames(like packets but not for local network)
Packet (Layer 3) → becomes → Frame (Layer 2)

### Error Detection
Checks if data got corrupted during transmission

### Layer 2 knows whom to send it to (which is MAC Address) not where to send it to (As it doesn't know the IP address of the destination)

---
# Layer 3 - Network 
This layer is responsible for finding the path and delivering data to the final destination using IP Address.

IT has 2 main Jobs:
1) Logical Addressing (IP)
Every device gets an IP Address
Example:

192.168.1.5  
8.8.8.8

This tells:
WHERE the data should go

2) Routing 
This decides which path should data take to reach the destination
Uses routers for this

---
# Layer 4 Transport 

Layer 4 is responsible for End-to-end communication between systems using ports

What does it actually Do?
1) Port Numbers
This is the MOST important part

Examples:

| Port | Service |
| ---- | ------- |
| 80   | HTTP    |
| 22   | SSH     |
| 445  | SMB     |

👉 Ports tell:

Which service to talk to

2) Protocols
Layer 4 uses:
- **TCP** (reliable)
- **UDP** (fast, no guarantee)

# Layer 5 - Session Layer

**Layer 5 (Session Layer)** is responsible for:

**Establishing, managing, and terminating communication sessions between two systems**

Session is continuous communication between two systems

### what does layer 5 actually do
### Session Establishment

👉 Starts communication

Example:

Login to website

---

### ✅ 2. Session Management

👉 Keeps communication active

Example:

You browse multiple pages without logging in again

---

### ✅ 3. Session Termination

👉 Ends communication

Example:

Logout or session timeout

---
# Layer 6

Layer 6 is responsible for:

👉 **Formatting, encoding, and encrypting data before sending**


- Handles **data translation, encryption, compression**

---

## 2. What Does It Actually Do?

### ✅ 1. Data Format Translation

- Converts data into readable format

Example:

- JSON
- HTML
- Images (JPEG, PNG)

---

### ✅ 2. Encryption / Decryption 🔥

- Protects data

Example:

HTTPS → uses SSL/TLS

---

### ✅ 3. Compression

- Reduces size of data

---

## 3. Easy Understanding

👉 Layer 6 = “Make data understandable and secure”

---

# Layer 7 — Application Layer

## 1. Definition

Layer 7 is responsible for:

👉 **Direct interaction with user applications**

- Provides services directly to users

---

## 2. What Does It Actually Do?

👉 This is where actual services run:

|Protocol|Use|
|---|---|
|HTTP|Websites|
|FTP|File transfer|
|SMTP|Email|
|SSH|Remote login|
|DNS|Domain resolution|

---

## 3. Easy Understanding

👉 Layer 7 = “What the user actually uses”

---

### 🧠 Example

When you open a website:

- Browser sends HTTP request
- Server responds

👉 That’s Layer 7