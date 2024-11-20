##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.10.88 -oA nmap2
```
```
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.88 -p 80 -v -oA nmap 
```
```
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Landing Page
|_http-server-header: Apache/2.4.18 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 5 disallowed entries 
| /webservices/tar/tar/source/ 
| /webservices/monstra-3.0.4/ /webservices/easy-file-uploader/ 
|_/webservices/developmental/ /webservices/phpmyadmin/
```

##### manual

- Found robots.txt when running gobuster
- Found 5 directories under robots.txt
![[Pasted image 20240902230542.png]]
- while others did not work, monstraCMS directory worked where I found /admin page
- Found a vulnerability for unauthenticated credential exposure on MonstraCMS 3.0.4 [Link](https://simpleinfoseccom.wordpress.com/2018/05/27/monstra-cms-3-0-4-unauthenticated-user-credential-exposure/)
- Found user `admin`
- Was successfully able to login as `admin:admin`
- 