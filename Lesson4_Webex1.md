# Web Exploitation day 1

## Server/Client Relationship
- Synchronous communications between user and services
- Not all data is not returned, client only receives what is allowed

## Hyper-Text Transfer Protocol (HTTP)
- Request/Response
  - Various tools to view:
    - tcpdump
    - wireshark
    - Developer Console
```
GET / HTTP/1.1
HTTP/1.1 200 OK
```

## HTTP Methods
- A Select Few:
  - GET
  - POST
  - HEAD
  - PUT
> https://tools.ietf.org/html/rfc2616

## HTTP Response Codes
- 10X == Informational
- 2XX == Success
- 30X == Redirection
- 4XX == Client Error
- 5XX == Server Error
> https://tools.ietf.org/html/rfc2616

## HTTP Packet Headers
> DEMO: Look at a header!
- Open a browser (on your opstation) and enter the Developer Console

## HTTP Fields
- User-Agent
- Referer
- Cookie
- Date
- Server
- Set-Cookie

## HTTP Method Notes
```
GET request can be utilized to pass data to the server using the URL string:
http://10.50.x.x/path/pathdemo.php?myfile=demo1
```

## Wget
- Recursively download
- Recover from broken transfers
- SSL/TLS support
```
wget -r -l2 -P /tmp ftp://ftpserver/
wget --save-cookies cookies.txt --keep-session-cookies --post-data 'user=1&password=2' https://website
wget --load-cookies cookies.txt -p https://website/interesting/article.php
```

## cURL
- Not recursive
- Can use pipes
- Upload ability
- Supports more protocols vs Wget, such as SCP & POP3
```
curl -o stuff.html https://web.site/stuff.html
curl 'https://web.site/submit.php' -H 'Cookie: name=123; settings=1,2,3,4,5,6,7' --data 'name=Stan' | base64 -d > item.png
```

## JavaScript (JS)
- Allows websites to interact with the client
  - JavaScript runs on the client’s machine
- Coded as .js files, or in-line of HTML

## JS Interaction
```
<script>
function myFunction() {
    document.getElementById("demo").innerHTML = "Paragraph changed.";
}
</script>
```
```
<script src="https://www.w3schools.com/js/myScript1.js"></script>
```

## JS in action
- DEMO: Lets take a look at Javademo.html
> http://10.50.XX.XX/java/Javademo.html


## Developer Console
- (Must be done from opstation!)

## Enumeration
- Robots.txt
- Legitimate surfing
- Tools:
  - NSE scripts
  - Nikto
  - Burp suite (outside class)

## Cross-Site Scripting (XSS) Overview
- Insertion of arbitrary code into a webpage, that executes in the browser of visitors
- Unsanitized GET, POST, and PUT methods allow JS to be placed on websites
- Often found in forums that allow HTML

## Reflected XSS
- Most common form of XSS
- Transient, occurs in error messages or search results
- Delivered through intermediate media, such as a link in an email
- Characters that are normally illegal in URLs can be Base64 encoded
- Below is what you see, but the server will decode as ```name=abc123```
  - http://example.com/page.php?name=dXNlcjEyMw

## Stored XSS
- Resides on vulnerable site
- Only requires user to visit page
```
<img src="http://invalid" onerror="window.open('http://10.50.XX.XX:8000/ram.png','xss','height=1,width=1');">
```

## Useful JavaScript Components
- Proof of concept (simple alert):
```
<script>alert('XSS');</script>
```
- Capturing Cookies
```document.cookie```
- Capturing Keystrokes
  - bind keydown and keyup
- Capturing Sensitive Data
```document.body.innerHTML```

## Server-Side injection
> Directory Traversal/Path Traversal
- Ability to read/execute outside web server’s directory
- Uses ```../../``` (relative paths) in manipulating a server-side file path
> view_image.php?file=../../etc/passwd

## Malicious File Upload
> Site allows unsanitized file uploads
- Server doesn’t validate extension or size
- Allows for code execution (shell)
- Once uploaded
  - Find your file
  - Call your file

## Command Injection
> Application on the server is vulnerable, allowing execution of arbitrary commands
- User input not validated
  - Common example is a SOHO router, with a web page to allow ping
Might contain the following in it’s code:
```
system("ping -c 1 ".$_GET["ip"]);
```
Run the following to chain/stack our arbitrary command
```
; cat /etc/passwd
```







