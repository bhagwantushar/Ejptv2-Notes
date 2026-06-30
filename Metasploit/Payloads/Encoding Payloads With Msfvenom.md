
Encode Payload
When you generate a payload using **msfvenom**, you’re basically creating a **malicious file (shellcode / reverse shell)**.

Problem:-
- Antivirus (AV) tools detect payloads using **signatures**
- Your payload has a **known pattern**
- AV says: ❌ “This is malicious → Block it

Encoding = **changing the appearance of the payload WITHOUT changing what it does**
Think like this:
- Original payload → `ATTACK`
- Encoded payload → `XJ3#@!` (looks different but same meaning internally)

 Goal:
- Bypass **signature-based detection**

## Solution → Encoding

Encoding = **changing the appearance of the payload WITHOUT changing what it does**

Think like this:
- Original payload → `ATTACK`
- Encoded payload → `XJ3#@!` (looks different but same meaning internally)

Goal:
- Bypass **signature-based detection**


## Shellcode 

The actual code that runs on target
- Opens reverse shell
- Executes commands

# How Encoding Works 

1. Take payload (shellcode)
2. Pass it through an **encoder**
3. Output becomes:
    - Obfuscated (changed structure)
    - Same functionality

---
# Common Encoder

### `shikata_ga_nai`

- Most commonly used encoder in Metasploit
- Polymorphic → changes every time

Meaning:
- Even if you generate payload twice → different output

# Basic Command Structure (Understand, don’t memorize)

msfvenom -p <payload> LHOST=<ip> LPORT=<port> -e <encoder> -i <iterations> -f <format>

---

## 🔍 Breakdown (IMPORTANT for exam)

- `-p` → payload (reverse shell etc.)
- `-e` → encoder (e.g., shikata_ga_nai)
- `-i` → number of encoding iterations
- `-f` → output format (exe, elf, raw)