# OP NOTES


## set up dynamic to scan known net
> on lin-ops
```
ssh -S /tmp/jump dynamo -O forward -D9050
```


## run a ping sweep from jump
> ping sweep from jump
```
for i in {1..254};do (ping -c 1 192.168.28.$i 2>/dev/null | grep "bytes from" &) ;done
```
> output
```
64 bytes from 192.168.28.1: icmp_seq=1 ttl=64 time=0.552 ms
64 bytes from 192.168.28.2: icmp_seq=1 ttl=63 time=1.09 ms
64 bytes from 192.168.28.3: icmp_seq=1 ttl=63 time=1.16 ms
64 bytes from 192.168.28.97: icmp_seq=1 ttl=64 time=0.082 ms
64 bytes from 192.168.28.99: icmp_seq=1 ttl=63 time=2.75 ms
64 bytes from 192.168.28.98: icmp_seq=1 ttl=63 time=4.27 ms
64 bytes from 192.168.28.100: icmp_seq=1 ttl=63 time=1.91 ms
64 bytes from 192.168.28.105: icmp_seq=1 ttl=63 time=0.634 ms
64 bytes from 192.168.28.111: icmp_seq=1 ttl=63 time=2.03 ms
64 bytes from 192.168.28.120: icmp_seq=1 ttl=63 time=2.04 ms
64 bytes from 192.168.28.129: icmp_seq=1 ttl=64 time=0.093 ms
64 bytes from 192.168.28.130: icmp_seq=1 ttl=63 time=1.41 ms
64 bytes from 192.168.28.131: icmp_seq=1 ttl=63 time=1.10 ms
```

## run a port scan on all ips in the net
> nmap scan
```
proxychains nmap 192.168.28.97,98,99,100,105,111,120
```
> results
```
Nmap scan report for 192.168.28.97
Host is up (0.00033s latency).
All 1000 scanned ports on 192.168.28.97 are closed

Nmap scan report for 192.168.28.98
Host is up (0.00049s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.99
Host is up (0.00047s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
53/tcp open  domain

Nmap scan report for 192.168.28.100
Host is up (0.00051s latency).
Not shown: 998 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.28.105
Host is up (0.00044s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
23/tcp   open  telnet
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.28.111
Host is up (0.00060s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1
8080/tcp open  http-proxy

Nmap scan report for 192.168.28.120
Host is up (0.00053s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
4242/tcp open  vrml-multi-use

Nmap done: 7 IP addresses (7 hosts up) scanned in 3.84 seconds
```

## banner grab all of the ports
> bannergrabs on .98
```
proxychains nc 192.168.28.98 53
```
> results
```
nothing
```

> bannergrabs on .99
```
proxychains nc 192.168.28.99 53
```
> results
```
nothing
```

> bannergrabs on .100
```
proxychains nc 192.168.28.100 80
proxychains nc 192.168.28.100 2222

```
> results
```
HTTP/1.1 400 Bad Request
Date: Tue, 17 Sep 2024 18:22:23 GMT
Server: Apache/2.4.29 (Ubuntu)
Content-Length: 301
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.29 (Ubuntu) Server at 127.0.0.1 Port 80</address>
</body></html>
```
```
SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3

Protocol mismatch.
```

> bannergrabs on .105
```
proxychains nc 192.168.28.105 21
proxychains nc 192.168.28.105 23
proxychains nc 192.168.28.105 2222
```
> results
```
220 ProFTPD 1.3.5 Server (Debian) [::ffff:192.168.28.105]

500 Invalid command: try being more creative
```
```
���� ��#��'
```
```
SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3

Protocol mismatch.
```

> bannergrabs on .111
```
proxychains nc 192.168.28.111 80
proxychains nc 192.168.28.111 2222
proxychains nc 192.168.28.111 8080
```
> results
```
HTTP/1.1 400 Bad Request
Date: Tue, 17 Sep 2024 18:24:13 GMT
Server: Apache/2.4.29 (Ubuntu)
Content-Length: 315
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.29 (Ubuntu) Server at consulting.site.donovia Port 80</address>
</body></html>
```
```
SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3

Protocol mismatch.
```
```
HTTP/1.1 400 Bad Request
Date: Tue, 17 Sep 2024 18:24:53 GMT
Server: Apache/2.4.29 (Ubuntu)
Content-Length: 315
Connection: close
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.29 (Ubuntu) Server at conference.site.donovia Port 80</address>
</body></html>

```

> bannergrabs on .120
```
proxychains nc 192.168.28.120 4242

```
> results
```
SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3

Protocol mismatch.
```


## wget the FTP ports
> wget on 105 ftp port
```
proxychains wget -r ftp://192.168.28.105
```
> results 
```
N/A
```

## Enumerate files
> cat the files
```
cat welcome.msg
cat ServerInitialization
cat rzKO4zkljcNJjLgt2SLa
```
> results
```
Welcome, archive user %U@%R !

The local time is: %T

This is an experimental FTP server.  If you have any unusual problems,
please report them via e-mail to <root@%L>.
```
```
PassTemporary
loginfirst
logout null bit
houseBeatFliesLOW
YourTempPassword

```
```
rzKO4zkljcNJjLgt2SLa
```


## set up forwards to view the web pages
> forwards to .100 and .111 web pages on local ports 8001,8002,8003
```
ssh -S /tmp/jump jump -O forward -L8001:192.168.28.100:80 -L8002:192.168.28.111:2222 -L8003:192.168.28.111:8080

```
> results
```
N/A
```


## view the webpages
> view webpages with firefox
```
firefox
-addresses
127.0.0.1:8001
127.0.0.1:8002
127.0.0.1:8003

```
> results
```
webpage under construction
A Donovia National Consulting page
a workshop to buy conference tickets
```











## 
>
```

```
> results
```

```



















