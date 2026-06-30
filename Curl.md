# cURL — Complete Notes 

---
# What is cURL?

`cURL` (Client URL) is a command-line tool used to transfer data between a client and a server using different protocols such as:

- HTTP
    
- HTTPS
    
- FTP
    
- SCP
    
- SMTP
    

It is mainly used for:

- API testing
    
- Web requests
    
- Downloading files
    
- Automation
    
- Cybersecurity testing
    
- Debugging web applications
    

---

# Basic Syntax

```bash
curl [options] [URL]
```

Example:

```bash
curl https://example.com
```

This sends a default GET request to the website.

---
# 1. GET Request

## Explanation

A GET request is used to retrieve data from a server.

## Command

```bash
curl https://jsonplaceholder.typicode.com/posts/1
```

## What Happens?

- cURL sends a GET request
    
- Server responds with data
    
- Output is displayed in terminal
    

## Example Output

```json
{
  "userId": 1,
  "id": 1,
  "title": "sample title"
}
```

---

# 2. View HTTP Headers Only

## Explanation

HTTP headers contain metadata about the response.

Useful for:

- Reconnaissance
    
- Server identification
    
- Security testing
    

## Command

```bash
curl -I https://example.com
```

## What `-I` Means

- Fetch headers only
    
- Do not fetch webpage body
    

## Example Output

```http
HTTP/1.1 200 OK
Server: nginx
Content-Type: text/html
```

---

# 3. Verbose Mode

## Explanation

Verbose mode shows detailed connection information.

Useful for:

- Debugging
    
- Seeing request/response headers
    
- TLS inspection
    

## Command

```bash
curl -v https://example.com
```

## What `-v` Shows

- DNS resolution
    
- TLS handshake
    
- Request headers
    
- Response headers
    

---

# 4. Save Output to File

## Explanation

Save server response into a file.

## Command

```bash
curl -o page.html https://example.com
```

## What `-o` Means

- Output response to file
    

## Result

Creates:

```text
page.html
```

---

# 5. Download File with Original Name

## Explanation

Downloads a file and keeps original filename.

## Command

```bash
curl -O https://example.com/file.zip
```

## What `-O` Means

- Save using remote server filename
    

---

# 6. POST Request

## Explanation

POST requests send data to a server.

Commonly used for:

- Login forms
    
- APIs
    
- Data submission
    

## Command

```bash
curl -X POST https://httpbin.org/post
```

## What `-X` Means

- Specify HTTP method
    

---

# 7. Send Form Data

## Explanation

Send key-value data like HTML forms.

## Command

```bash
curl -X POST \
-d "username=admin&password=1234" \
https://httpbin.org/post
```

## What `-d` Means

- Send request body data
    

## Equivalent HTML Form

```html
<form method="POST">
```

---

# 8. Send JSON Data

## Explanation

Modern APIs usually accept JSON.

## Command

```bash
curl -X POST \
-H "Content-Type: application/json" \
-d '{"name":"John","age":25}' \
https://httpbin.org/post
```

---

# Understanding the Parts

## `-H`

```bash
-H "Content-Type: application/json"
```

Adds a custom HTTP header.

---

## `Content-Type`

Tells the server what type of data is being sent.

Example:

```text
application/json
```

---

## `-d`

```bash
-d '{"name":"John"}'
```

Sends request body data.

---

# 9. Basic Authentication

## Explanation

Some servers require username/password authentication.

## Command

```bash
curl -u admin:password https://example.com
```

## What `-u` Means

- Username and password authentication
    

---

# 10. Bearer Token Authentication

## Explanation

APIs commonly use Bearer tokens.

## Command

```bash
curl -H "Authorization: Bearer TOKEN_HERE" \
https://api.example.com/data
```

## Purpose

Authenticates API access.

---

# 11. PUT Request

## Explanation

PUT updates existing data.

## Command

```bash
curl -X PUT \
-H "Content-Type: application/json" \
-d '{"name":"Updated"}' \
https://httpbin.org/put
```

---

# 12. DELETE Request

## Explanation

DELETE removes resources from server.

## Command

```bash
curl -X DELETE https://httpbin.org/delete
```

---

# 13. Follow Redirects

## Explanation

Some websites redirect automatically.

Example:

```text
http://example.com → https://example.com
```

## Command

```bash
curl -L http://example.com
```

## What `-L` Means

- Follow redirects
    

---

# 14. Cookies

---

## Save Cookies

### Explanation

Save session cookies to file.

### Command

```bash
curl -c cookies.txt https://example.com
```

---

## Use Saved Cookies

### Explanation

Reuse authenticated session.

### Command

```bash
curl -b cookies.txt https://example.com/dashboard
```

---

# 15. User-Agent Spoofing

## Explanation

Pretend to be a browser.

Useful for:

- Bypassing simple restrictions
    
- Testing applications
    

## Command

```bash
curl -A "Mozilla/5.0" https://example.com
```

## What `-A` Means

- Set User-Agent
    

---

# 16. Upload File

## Explanation

Upload files using multipart forms.

## Command

```bash
curl -F "file=@test.txt" https://httpbin.org/post
```

## What `-F` Means

- Multipart form upload
    

---

# 17. Check Security Headers

## Explanation

Useful in web security assessments.

## Command

```bash
curl -I https://example.com
```

## Important Headers

|Header|Purpose|
|---|---|
|Strict-Transport-Security|HTTPS enforcement|
|Content-Security-Policy|XSS protection|
|X-Frame-Options|Clickjacking protection|

---

# 18. API Testing Example

## Command

```bash
curl -X GET \
-H "Authorization: Bearer token_here" \
https://api.example.com/users
```

## What Happens?

- Sends GET request
    
- Adds authorization header
    
- Receives API response
    

---

# 19. Download and Resume Interrupted Download

## Command

```bash
curl -C - -O https://example.com/bigfile.iso
```

## What `-C -` Means

- Resume interrupted download
    

---

# 20. Ignore SSL Certificate Errors

## Explanation

Useful in labs/testing environments.

⚠️ Do NOT use in production.

## Command

```bash
curl -k https://self-signed-site.com
```

## What `-k` Means

- Ignore invalid SSL certificates
    

---

# Important Options Cheat Sheet

|Option|Meaning|
|---|---|
|-X|HTTP method|
|-H|Add header|
|-d|Send data|
|-I|Headers only|
|-v|Verbose|
|-L|Follow redirects|
|-o|Save output|
|-O|Save with original filename|
|-u|Basic auth|
|-A|User-Agent|
|-c|Save cookies|
|-b|Send cookies|
|-F|Upload file|
|-k|Ignore SSL errors|

---

# Cybersecurity Use Cases

## Reconnaissance

```bash
curl -I https://target.com
```

Find:

- Server type
    
- Technologies
    
- Security headers
    

---

## API Testing

```bash
curl -X POST \
-H "Content-Type: application/json" \
-d '{"username":"admin"}' \
https://api.target.com/login
```

---

## Session Testing

```bash
curl -b cookies.txt https://target.com/profile
```

---

# Common Beginner Mistakes

---

## Missing Quotes

Wrong:

```bash
-H Content-Type: application/json
```

Correct:

```bash
-H "Content-Type: application/json"
```

---

## Forgetting JSON Header

Without:

```text
Content-Type: application/json
```

Server may reject request.

---

# Mental Model

Think of cURL as:

```text
A command-line web browser and API client
```

Instead of clicking buttons in browser:

- You manually create requests
    
- Control headers
    
- Send payloads
    
- Analyze responses
    

This is why cURL is extremely important in:

- Penetration testing
    
- API security
    
- Bug bounty
    
- DevOps
    
- Automation
    
- SOC operations