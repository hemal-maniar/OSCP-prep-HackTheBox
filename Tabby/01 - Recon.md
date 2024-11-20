##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.10.194 -oA nmap2
```
```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
8080/tcp open  http    Apache Tomcat
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.194 -p 22,80,8080 -v -oA nmap
```
```

PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 45:3c:34:14:35:56:23:95:d6:83:4e:26:de:c6:5b:d9 (RSA)
|   256 89:79:3a:9c:88:b0:5c:ce:4b:79:b1:02:23:4b:44:a6 (ECDSA)
|_  256 1e:e7:b9:55:dd:25:8f:72:56:e8:8e:65:d5:19:b0:8d (ED25519)
80/tcp   open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Mega Hosting
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 338ABBB5EA8D80B9869555ECA253D49D
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
8080/tcp open  http    Apache Tomcat
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Apache Tomcat
| http-methods: 
|_  Supported Methods: OPTIONS GET HEAD POST
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

##### manual
- Added megahosting.htb to `/etc/hosts`
- Found a page displaying a statement at http://megahosting.htb/news.php?file=statement
- This is vulnerable to LFI on http://megahosting.htb/news.php?file=../../../../etc/passwd
- Found user `ash`
![[Pasted image 20240903194536.png]]
- Found a guide on hacktricks for pentesting tomcat to discover `tomcat-users.xml` file
https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/tomcat#post
![[Pasted image 20240903210158.png]]

- Using this password, logged into Tomcat Virtual Host Manager
`tomcat:$3cureP4s5w0rd123!`