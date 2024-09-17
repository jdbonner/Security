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
proxychains nmap -T5 --script=banner <ip>
proxychains nmap -T5 --script=http-enum <ip>
proxychains nmap -T5 --script=http-enum.nse <ip>


## finding a script
ls -l /usr/share/nmap/scripts | grep "something"




























