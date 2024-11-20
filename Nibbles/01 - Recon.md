##### nmap

- All port scan
```bash
sudo nmap -sS -Pn -T5 -p- 10.10.10.75 -oA nmap2
```
Identified services
```

```

- Service scan
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c4:f8:ad:e8:f8:04:77:de:cf:15:0d:63:0a:18:7e:49 (RSA)
|   256 22:8f:b1:97:bf:0f:17:08:fc:7e:2c:8f:e9:77:3a:48 (ECDSA)
|_  256 e6:ac:27:a3:b5:a9:f1:12:3c:34:a5:5d:5b:eb:3d:e9 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

##### manual

- Navigated to http://10.10.10.75
- Found a comment for /nibbleblog directory under the webpage
- README reveals it is running nibbleblog v4.0.3
- Found the user `admin` in /nibbleblog/content/private/users.xml
![[Pasted image 20240831190223.png]]
- Was able to successfully log in as `admin:nibbles`