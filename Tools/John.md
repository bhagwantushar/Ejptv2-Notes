
John is a password cracking tool
Its job is:
```
Hash/File → Password
```
Examples:
```
MD5 hash
SHA1 hash
bcrypt hash
ZIP file
RAR file
SSH private key
Linux shadow hash
```
John tries passwords until it finds the correct one.


John Command Structure

Almost everything follows:
```
john <target> [options]
```
Examples:
```
john hash.txt
```

```
john hash.txt --wordlist=rockyou.txt
```

```
john hash.txt --incremental
```



Attack Modes


1. Wordlist Attack

Most common.
```
john hash.txt --wordlist=rockyou.txt
```
John tries:
```
123456
password
qwerty
welcome
...
```
against the hash.


2. Rules Attack

Takes a wordlist and mutates words.
```
john hash.txt --wordlist=rockyou.txt --rules
```
Example:
Word:
```
password
```
John tries:
```
Password
password1
Password1
PASSWORD
```
Much more powerful.


3. Incremental Attack

John's brute force mode.
```
john hash.txt --incremental
```
Tries:
```
a
b
c
...
aa
ab
...
```
Very slow.
Use only when wordlists fail.


4. Single Crack Mode

Unique to John.
```
john hash.txt --single
```
Uses information from usernames.
Example:
```
admin
administrator
root
```
Generates guesses automatically.


Cracking ZIP Files

Very common in CTFs.
Extract hash:
```
zip2john secret.zip > zip.hash
```
Crack:
```
john zip.hash --wordlist=rockyou.txt
```


Cracking RAR Files

```
rar2john secret.rar > rar.hash
```

```
john rar.hash --wordlist=rockyou.txt
```


Cracking SSH Keys

```
ssh2john id_rsa > ssh.hash
```

```
john ssh.hash --wordlist=rockyou.txt
```



Format Detection

This is the John equivalent of Hashcat modes.
Hashcat:
```
hashcat -m 0
```
John:
```
john --format=Raw-MD5
```
Examples:
Hash Type
John Format
MD5
Raw-MD5
SHA1
Raw-SHA1
NTLM
NT
bcrypt
bcrypt
SHA512Crypt
sha512crypt
