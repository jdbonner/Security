# Tunnels

## Setting up the connection
- set up connection to jump box
```ssh -MS /tmp/jump student@10.50.35.126```
- the /tmp/jump file is a socket

## Scanning IPs
- scan ips
```for i in {1..254};do (ping -c 1 192.168.28.$i 2>/dev/null | grep "bytes from" &) ;done```
```
64 bytes from 192.168.28.1: icmp_seq=1 ttl=64 time=0.246 ms
64 bytes from 192.168.28.3: icmp_seq=1 ttl=63 time=1.80 ms
64 bytes from 192.168.28.2: icmp_seq=1 ttl=63 time=62.6 ms
64 bytes from 192.168.28.97: icmp_seq=1 ttl=64 time=0.102 ms
64 bytes from 192.168.28.99: icmp_seq=1 ttl=63 time=5.73 ms
64 bytes from 192.168.28.98: icmp_seq=1 ttl=63 time=7.33 ms
64 bytes from 192.168.28.100: icmp_seq=1 ttl=63 time=4.31 ms
64 bytes from 192.168.28.105: icmp_seq=1 ttl=63 time=0.618 ms
64 bytes from 192.168.28.111: icmp_seq=1 ttl=63 time=1.90 ms
64 bytes from 192.168.28.120: icmp_seq=1 ttl=63 time=2.05 ms
64 bytes from 192.168.28.129: icmp_seq=1 ttl=64 time=0.087 ms
64 bytes from 192.168.28.130: icmp_seq=1 ttl=63 time=1.75 ms
64 bytes from 192.168.28.131: icmp_seq=1 ttl=63 time=1.66 ms
```
## Dynamic tunnel
- now we need to set up the dynamic
```ssh -S /tmp/jump jump -O forward -D9050```
## Port Scans
- scan ports
```proxychains nmap 192.168.28.97,98,100,105```
```
Nmap scan report for 192.168.28.98
Host is up (0.00055s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.100
Host is up (0.00053s latency).
Not shown: 998 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.28.105
Host is up (0.00051s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
23/tcp   open  telnet
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.28.111
Host is up (0.00057s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1
8080/tcp open  http-proxy

Nmap scan report for 192.168.28.120
Host is up (0.00058s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
4242/tcp open  vrml-multi-use

> banner grab ports
proxychains nmap 192.168.28.100 80
proxychains nmap 192.168.28.100 2222
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
```ssh -S /tmp/jump jump -O forward -L2222:192.168.28.100:80 -L3333:192.168.28.100:2222```
- you can forward to multiple ips

## Opening websites through the forward
- we can access the website via firefox on our lin-ops workstations 
```firefox```
- enter the loopback and the port 127.0.0.1:2222
## Tunneling to another device
- gonna use the shit out of this to authenticate to new system
```ssh -MS /tmp/t1 creds@127.0.0.1 -p 3333```
## Forwarding through the new tunnel
- theoretically after you scan the new net you find 192.168.50.10,20,30 - port 22
```ssh -S /tmp/t1 t1 -O forward -L6666:192.168.50.10:22 -L7777:192.168.50.20:22```
## Stepping through the tunnel
- making next step to tunnel
```ssh -MS /tmp/t2 creds@127.0.0.1 -p 6666```
































