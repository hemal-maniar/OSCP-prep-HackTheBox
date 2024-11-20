##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.10.73 -oA nmap2
```
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.73 -p 22,80 -v -oA nmap 
```
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 36:c0:0a:26:43:f8:ce:a8:2c:0d:19:21:10:a6:a8:e7 (RSA)
|   256 cb:20:fd:ff:a8:80:f2:a2:4b:2b:bb:e1:76:98:d0:fb (ECDSA)
|_  256 c4:79:2b:b6:a9:b7:17:4c:07:40:f3:e5:7c:1a:e9:dd (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Falafel Lovers
|_http-favicon: Unknown favicon MD5: B8A9422F95F0D71B26D25CE15206BB79
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/*.txt
|_http-server-header: Apache/2.4.18 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

##### manual

- Added `falafel.htb` to `/etc/hosts`
- Found /cyberlaw.txt using gobuster
![[Pasted image 20240904123354.png]]
- Tested the login.php page and tried different usernames and found `admin` & `chris` as valid usernames
- Cyberlaw.txt says that `chris` was able to log in without a password which indicates it could be vulnerable to SQL injection
- Running SQLmap
```bash
sqlmap -r r.txt --risk=3 --level=5 --batch --string "Wrong identification" -p username
```
- dbs
![[Pasted image 20240904123559.png]]
- tables
![[Pasted image 20240904123644.png]]
- table dump
![[Pasted image 20240904123740.png]]

`chris` has set password to `juggling`
![[Pasted image 20240904123842.png]]

Took reference from a walkthrough, but it mentions emphasis on juggling part and I found [PHP Type Juggling](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Type%20Juggling/README.md)
 ## Magic Hashes

> Magic hashes arise due to a quirk in PHP's type juggling, when comparing string hashes to integers. If a string hash starts with "0e" followed by only numbers, PHP interprets this as scientific notation and the hash is treated as a float in comparison operations.

Our admin hash also starts with 0e followed by only numbers.
![[Pasted image 20240904133037.png]]
Using the Magic Number `240610708`, I was able to log in as `admin`

When a valid URL is given, we get output 
![[Pasted image 20240904133331.png]]
