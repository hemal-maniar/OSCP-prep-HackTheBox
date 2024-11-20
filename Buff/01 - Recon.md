##### nmap

All port scan
```bash
sudo nmap -sV -p- 10.10.10.198 -v -oA nmap2
```
```
PORT     STATE SERVICE    VERSION
7680/tcp open  pando-pub?
8080/tcp open  http       Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.198 -p 7680,8080 -v -oA nmap
```
```
PORT     STATE SERVICE    VERSION
7680/tcp open  pando-pub?
8080/tcp open  http       Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.6
|_http-title: mrb3n's Bro Hut
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
```

##### manual

Navigated to http://10.10.10.198:8080/contact.php
![[Pasted image 20240908110753.png]]

Found a public exploit on [ExploitDB](https://www.exploit-db.com/exploits/48506) for Gym Management System 1.0