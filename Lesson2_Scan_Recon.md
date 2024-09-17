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










