
### HTTP Requests 
An HTTP Request is a message sent by a client(usually a web browser) to a web server asking for a resource such as:

- A webpage 
- An image
-  API data
-  a file
The server processes the request and returns an HTTP response.

# Basic HTTP Communication

```
Browser  →  HTTP Request  →  Web ServerBrowser  ← HTTP Response ←  Web Server
```

Example:  
When you open:

```
https://www.google.com
```

your browser sends an HTTP request to the server.

# Structure of an HTTP Request

According to the course material, an HTTP request has three main parts:

1. Request Line
2. Request Headers
3. Request Body

# Full HTTP Request Example

```
GET / HTTP/1.1
Host: www.google.com
User-Agent: Mozilla/5.0Accept: text/html
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

# Request Line

The first line of the request is called the **Request Line**.

Example:

```
GET / HTTP/1.1
```

It contains 3 components:

|Component|Meaning|
|---|---|
|GET|HTTP Method|
|/|URL/Path|
|HTTP/1.1|HTTP Protocol Version|

| Method  | Purpose                   |
| ------- | ------------------------- |
| GET     | Retrieve data             |
| POST    | Submit data               |
| PUT     | Replace/update resource   |
| PATCH   | Partially update resource |
| DELETE  | Remove resource           |
| HEAD    | Retrieve headers only     |
| OPTIONS | Show supported methods    |