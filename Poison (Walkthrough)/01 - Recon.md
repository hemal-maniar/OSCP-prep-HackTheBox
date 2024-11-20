##### nmap

All port scan
```bash
sudo nmap -sS -T5 -p- 10.10.10.84 -oA nmap2 -v
```
```
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

Service scan
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2 (FreeBSD 20161230; protocol 2.0)
| ssh-hostkey: 
|   2048 e3:3b:7d:3c:8f:4b:8c:f9:cd:7f:d2:3a:ce:2d:ff:bb (RSA)
|   256 4c:e8:c6:02:bd:fc:83:ff:c9:80:01:54:7d:22:81:72 (ECDSA)
|_  256 0b:8f:d5:71:85:90:13:85:61:8b:eb:34:13:5f:94:3b (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((FreeBSD) PHP/5.6.32)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_http-server-header: Apache/2.4.29 (FreeBSD) PHP/5.6.32
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
Service Info: OS: FreeBSD; CPE: cpe:/o:freebsd:freebsd
```
##### manual

- Navigated to website
![[Pasted image 20240901131533.png]]
Seems like it allows us to run php scripts
- listfiles.php
![[Pasted image 20240901131614.png]]
Found a file pwdbackup.txt
- pwdbackup.txt
![[Pasted image 20240901131647.png]]
- Using the same functionality, LFI is possible on the webserver
![[Pasted image 20240901132318.png]]

Using PHP wrapper class to extract information base64 encoded
`http://10.10.10.84/browse.php?file=php://filter/convert.base64-encode/resource=/etc/passwd`

We know the password is encoded 13 times. Base64 decoded 13 times and found a valid password
`Charix!2#4%6&8(0`

`charix:Charix!2#4%6&8(0`