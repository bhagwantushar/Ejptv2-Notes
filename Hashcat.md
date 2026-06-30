Hashcat is a password-cracking tool. It takes a hash and tries a candidate passwords until it finds one that produces the same hash.

Example:

Password:

```
password
```

MD5 hash:

```
5f4dcc3b5aa765d61d8327deb882cf99
```

Hashcat's job is to discover that the hash corresponds to the password `password`.

## Syntax 

```
hashcat -m HASH_TYPE -a ATTACK_MODE hashes.txt wordlist.txt
```

For now, remember:

|Option|Meaning|
|---|---|
|`-m`|Hash type|
|`-a`|Attack type|
|`hashes.txt`|File containing hashes|
|`wordlist.txt`|Password list|

## Creating a Hash

Create a file:

```
echo "5f4dcc3b5aa765d61d8327deb882cf99" > hashes.txt
```

Verify:

```
cat hashes.txt
```

Output:

```
5f4dcc3b5aa765d61d8327deb882cf99
```

### Identify the hash type

Install:

```
sudo apt install hashid
```

Run -> hashid : <hash>

Example:

 hash-identifier
   #########################################################################
   #     __  __                     __           ______    _____           #
   #    /\ \/\ \                   /\ \         /\__  _\  /\  _ `\         #
   #    \ \ \_\ \     __      ____ \ \ \___     \/_/\ \/  \ \ \/\ \        #
   #     \ \  _  \  /'__`\   / ,__\ \ \  _ `\      \ \ \   \ \ \ \ \       #
   #      \ \ \ \ \/\ \_\ \_/\__, `\ \ \ \ \ \      \_\ \__ \ \ \_\ \      #
   #       \ \_\ \_\ \___ \_\/\____/  \ \_\ \_\     /\_____\ \ \____/      #
   #        \/_/\/_/\/__/\/_/\/___/    \/_/\/_/     \/_____/  \/___/  v1.2 #
   #                                                             By Zion3R #
   #                                                    www.Blackploit.com #
   #                                                   Root@Blackploit.com #
   #########################################################################
--------------------------------------------------
 HASH: 5f4dcc3b5aa765d61d8327deb882cf99

Possible Hashs:
[+] MD5
[+] Domain Cached Credentials - MD4(MD4(($pass)).(strtolower($username)))


