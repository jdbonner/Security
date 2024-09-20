# Penetration Testing
https://sec.cybbh.io/public/security/latest/lessons/lesson-1-pentest_sg.html
## Penetration Testing

### Phase 1: Mission Definition
- Define mission goals and targets
- Determine scope of mission
- Define RoE


### Phase 2: Recon
- Information gathering about the target through public sources

### Phase 3: Footprinting
- Accumulate data through scanning and/or interaction with the target/target resources

### Phase 4: Exploitation & Initial Access
- Gain an initial foothold on network

### Phase 5: Post-Exploitation
- Establish persistence
- Escalate privileges
- Cover your tracks
- Exfiltrate target data

### Phase 6: Document Mission
- Document and report mission details


## Penetration Test Reporting
- Operation Notes (OPNOTES) vs Formalized Reporting

## Penetration Test Reporting
- Executive Summary
- Technical Summary

## Penetration Test Reporting
- Reasons to report
- What to report
- Screen captures


# Scanning and Reconnaissance
https://sec.cybbh.io/public/security/latest/lessons/lesson-2-recon_sg.html

## Open Source Intelligence
- During the lesson we will review the following topics:
- Appropriate Documentation Practices
- Use of Collected Data
- Collection Methods


## DoD States:
"produced from publicly available information that is collected, exploited, and disseminated in a timely manner to an appropriate audience for addressing a specific intelligence requirement."


## Documentation
- Why is it important?
- What should we include in documentation?

## OSINT Process Results
![](https://github.com/jdbonner/Security/blob/main/images/OSINT_Process_Results.png?raw=true)

## Collection and Use
- What do we want to collect?
- How can it be used in operations?

## Limitations on Collection
- Are there rules that guide our operations and collection parameters?
- What are important factors when collecting data about a target?

## Data to Collect
- Web Data
- Sensitive Data
- Publicly Accessible
- Social Media
- Domain and IP Data


## Data to Collect
- Web Data
  - Cached Content, Analytics, Proxy Web Application, Command Line Interrogation
- Sensitive Data
  - Business Data, Profiles, Non-Profits/Charities, Business Filings, Historical and Public Listings
- Publicly Accessible
  - Physical Addresses, Phone Numbers, Email Addresses, User Names, Search Engine Data, Web and Traffic Cameras, Wireless Access Point Data
- Social Media
  - Twitter, Facebook, Instagram, People Searches, Registry and Wish Lists
- Domain and IP Data
  - DNS Registration, IP Address Assignments, Geolocation Data, Whois


## Hyper-Text Markup Language (HTML)
> Standardized markup language for browser interpretation of webpages
- Client-side interpretation (web browser)
- Utilizes elements (identified by tags)
- Typically redirects to another page for server-side interaction
- Cascading Stylesheets (CSS) for page themeing

## HTML
- DEMO: Simple HTML page
> http://10.50.XX.XX/webexample/htmldemo.html

## Demonstration
- Data collection through scraping

## Scraping Data
- Prep
```pip install lxml requests```
- Script
```
#!/usr/bin/python
import lxml.html
import requests

page = requests.get('http://quotes.toscrape.com')
tree = lxml.html.fromstring(page.content)

authors = tree.xpath('//small[@class="author"]/text()')

print ('Authors: ',authors)
```
- What will it output?
```
Authors:  ['Albert Einstein', 'J.K. Rowling', 'Albert Einstein', 'Jane Austen', 'Marilyn Monroe', 'Albert Einstein', u’Andr\xe9 Gide', 'Thomas A. Edison', 'Eleanor Roosevelt', 'Steve Martin']
```

## Advanced Scanning Techniques
- Host Discovery
  - Find hosts that are online
- Port Enumeration
  - Find ports for each host that is online
- Port Interrogation
  - Find what service is running on each open/available port

## Demonstration
- Advanced Scanning Techniques

## NMAP Scripting Engine
> During the lesson we will review the following topics:
-  Benefits of Scanning with Scripts
- Script Management and Utilization
- Usage and Examples

## Nmap Project States:
"(It) allows users to write (and share) simple scripts to automate a wide variety of networking tasks. Those scripts are then executed in parallel with the speed and efficiency you expect from Nmap."

## Benefits
- Why use scripts, instead of normal scanning options?
- Why are scripts important?

## Main Benefits
- Network Discovery
- Sophisticated Version Detection
- Vulnerability Detection
- Backdoor Detection
- Vulnerability Exploitation


## Script Management
- Scripts are stored in a subdirectory of the Nmap data directory by default:
```/usr/share/nmap/scripts```

## Demonstration
- Nmap Familiarization


## Usage and Examples
```
nmap --script <filename>|<category>|<directory>
nmap --script-help "ftp-* and discovery"
nmap --script-args <args>
nmap --script-args-file <filename>
nmap --script-help <filename>|<category>|<directory>
nmap --script-trace
```

## Demonstration
- Usage of Nmap NSE


# Exploitation research
https://sec.cybbh.io/public/security/latest/lessons/lesson-3-research_sg.html

## Initial Access
- What is initial access?
- What is now the most common method for gaining initial access?
> Phishing!

## Initial Access
- What are some other techniques to gain initial access?

## Introduction to Exploit Research
- Transition from reconnaissance to weaponization
- Leverage intelligence/data about network
- Pair vulnerabilities to exploits
- Align exploits to operational objectives

## Research
- Open sources
- Organizational capabilities

## Capabilities
- Mission Objectives drive requirements
  - Collection
  - Effects
- Additional functionality to fulfill requirements
- Communications security (COMSEC)

## Testing
- Exploit Development occurs from vulnerability pairing and mission-drivens requirement
  - Test and verify success
- Testing provides a number of benefits:
  - Faster time to breakout of initial foothold
  - Reduced risk of detection and/or tool failure
  - Improved recovery times

## Plan
- Procure Hardware and software
- Assign developer
- Assign a tester to develop TTPs and break it
- Document testing results
- Testing environment


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

# Web Exploitation day 2

## SQL
- S tructured Q uery L anguage - ANSI Standard
- Additional commands added by vendors
- Relational

## Standard Commands
- SELECT - Extracts data from a database
- UNION - Used to combine the result-set of two or more SELECT statements
- USE - Selects the DB to use
- UPDATE - Updates data in a database
- DELETE - Deletes data from a database
- INSERT INTO - Inserts new data into a database
- CREATE DATABASE - Creates a new database
- ALTER DATABASE - Modifies a database
- CREATE TABLE - Creates a new table
- ALTER TABLE - Modifies a table
- DROP TABLE - Deletes a table
- CREATE INDEX - Creates an index (search key)
- DROP INDEX - Deletes an index
- https://www.w3schools.com/SQL/sql_syntax.asp


## DB Interactions
- DEMO: SQL Commands

## Activity
- SQLBOLT
- Interactive tutorials 1-11 and 13
- https://sqlbolt.com/

## SQL Injection - Considerations
- Requires Valid SQL Queries
- Fully patched systems can be vulnerable due to misconfiguration
- Input Field Sanitization
- String vs Integer Values
- Is information_schema Database available?
- GET Request versus POST Request HTTP methods

## Unsanitized vs Sanitized Fields
- Unsanitized: input fields can be found using a Single Quote ⇒ '
- Will return extraneous information
- ' closes a variable, to allow for additional statements/clauses
- May show no errors or generic error (harder Injection)
- Sanitized: input fields are checked for items that might harm the database (Items are removed, escaped, or turned into a single string)
- Validation: checks inputs to ensure it meets a criteria (String doesn’t contain ')


## Server-Side Query Processing
- User enters JohnDoe243 in the name form field and pass1234 in the pass form field.
- The Server-Side Query that would be passed to MySQL from PHP would be:
- BEFORE INPUT:
  - SELECT id FROM users WHERE name=‘$name’ AND pass=‘$pass’;
- AFTER INPUT:
  - SELECT id FROM users WHERE name=‘JohnDoe243’ AND pass=‘pass1234’;


## Example - Injecting Your Statement
- User enters tom' OR 1='1 in the name and pass fields.
- Truth Statement: tom ' OR 1='1
- Server-Side query executed would appear like this:
- SELECT id FROM users WHERE name=‘tom' OR 1='1’ AND pass=‘tom' OR 1='1’

## SQL Injection Validation
- DEMO: SQL Injection
- http://10.50.XX.XX


## Stacking Statements
- Chaining multiple statements together using a semi-colon ;
- SELECT * FROM user WHERE id=‘Johnny'; DROP TABLE Customers; --’


## Nesting statements
- Some Web Application + SQL Database combinations do not allow stacking, such as PHP and MySQL.
- Though they may allow for nesting a statement within an existing one:
- php?key=<value> UNION SELECT 1,column_name,3 from information_schema.columns where table_name = 'members'


## Ignore the rest
- Using # or -- tells the Database to ignore everything after
- Server-Side Query:
- SELECT product FROM item WHERE id = $select limit 1;
- Input to Inject:
- 1 or 1=1; #
- Server-Side Query becomes:
- SELECT product FROM item WHERE id = 1 or 1=1; # limit 1;



## SQL Injection (Nesting)
- DEMO: SQL Injection (Nesting Statements)
- http://10.50.XX.XX/Union.html


## Blind Injection
- Inlcudes Statements to determine how DB is configured
  - Columns in Output
  - Can we return errors
  - Can we return expected Output
- Used when unsanitized fields give generic error or no messages
- Normal Query to pull expected output:
- php?item=4
- Blind injection for validation:
- php?item=4 OR 1=1
- Try ALL combinations! item=1, item=2, item=3, etc.


## Abuse The Client (GET METHOD)
- Passing injection through the URL:
- After the .php?item=4 pass your UNION statement
- prices.php?item=4 UNION SELECT 1,2
- prices.php?item=4 UNION SELECT 1,2,@@version
- What is @@version?


## Abuse The Client (Enum)
- Identifying the schema leads to detailed queries to enumerate the DB
- Research Database Schemas and what information they provide
- php?item=4 UNION SELECT 1,table_name,3 from information_schema.tables where table_schema=database()
- What are information_schema and database()?


## SQL Injection (Database Enumeration)
- DEMO: SQL Injection (Database Enumeration)
- http://10.50.XX.XX/Union.html


## Defending Against
- Validate inputs! Methods differ depending on software
- concatenate : turns inputs into single strings or escape characters
- PHP: mysql_real_escape_string
- SQL: sqlite3_prepare()

# Reverse Engineering
https://sec.cybbh.io/public/security/latest/lessons/lesson-6-reverse_sg.html

## X86_64 Assembly
- There are 16 general purpose 64-Bit registers
- %rax      the first return register
- %rbp      the base pointer that keeps track of the base of the stack
- %rsp      the stack pointer that points to the top of the stack
- You will see arguments passed to functions as something like:```[%ebp-0x8]```

## X86_64 Assembly - Common Terms
- Heap                Memory that can be allocated and deallocated
- Stack               A contiguous section of memory used for passing arguments
- General Register    A multipurpose register that can be used by either programmer or user to store data or a memory location address
- Control Register    A processor register that changes or controls the behavior of a CPU
- Flags Register      Contains the current state of the processor

## X86_64 Assembly - Memory Offset
- There is one instruction pointer register that points to the memory offset of the next instruction in the code segment:
```
------------------------------------------------------------------------------------------------------------------
64-Bit  -  Lower 32 bits  -  Lower 16 bits  -  Descrition
RIP     -  EIP            -  IP             -  Instruction Pointer; holds address for next instruction to be executed
--------------------------------------------------------------------------------------------------------------------
```

## X86_64 Assembly - Common Instruction Pointers
- MOV     move source to destination
- PUSH    push source onto stack
- POP     Pop top of stack to destination
- INC     Increment source by 1
- DEC     Decrement source by 1
- ADD     Add source to destination
- SUB     Subtract source from destination
- CMP     Compare 2 values by subtracting them and setting the %RFLAGS register. ZeroFlag set means they are the same.
- JMP     Jump to specified location
- JLE     Jump if less than or equal
- JE      Jump if equal


## Reverse Engineering Workflow (Software)
- Static
- Behavioral
- Dynamic
- Disassembly
- Document Findings
- Reverse Engineering Workflow
```
https://git.cybbh.space/sec/public/-/jobs/artifacts/master/raw/guides/Reverse_engineering_workflow.pdf?job=genpdf
```
![](https://github.com/jdbonner/Security/blob/main/images/reverse_engine_workflow.png)


## Portable Executable Patching / Software Analysis
- Perform Debugging and Disassembly
- Find the Success/Failure
- Adjust Instructions
- Apply Patch and Save
- Execute Patched Binary


## Assemlby example1
```
main:
  mov rax, 16         //move in rax the value of 16.
  push rax            //push the value of rax (16) onto the stack. stack grows by     8 bytes.
  jmp mem2            //jump to mem2 function

mem1:       
  mov rax, 8          //move in rax the value of 8
  ret                 //return the value of what is in the first return registry.

mem2:   
  pop r8              //pop the value at the top of the stack (16) into r8
  cmp rax, r8         //compare to the value of rax (16) the value of r8 (16). They are equal; zero flag is set.
  je mem1             //zero flag from last instruction is set. jump to mem1 function.
```
## Assembly example 2
```
main:
  mov rcx, 25       //move into rcx the value of 25
  mov rbx, 62       //move into rbx the value of 62
  jmp mem1          //jump to location mem1

mem1:
  sub rbx, 40       //subtract from rbx the value of 40, rbx is now 22
  mov rsi, rbx      //move rsi into rbx
  cmp rcx, rsi      //compare the value of rcx (25) to the value of rsi (22). flag indicating less than is set.
  jle mem2          //jump if less than or equal to flag is set. rsi is less than rcx, jump to mem2.

mem2:
  mov rax, 0        //move into rax the value of 0
  ret               //returns the value of what is in the first return registry. returns 0
```



























