#### nmap
```bash
sudo nmap -sC -sV -oN editorial/nmap 10.10.11.20
```
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 0d:ed:b2:9c:e2:53:fb:d4:c8:c1:19:6e:75:80:d8:64 (ECDSA)
|_  256 0f:b9:a7:51:0e:00:d5:7b:5b:7c:5f:bf:2b:ed:53:a0 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to http://editorial.htb
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
- Ran an `nmap` scan for all TCP ports but no other ports other than 22 & 80 are open.

Since the root page redirects to `http://editorial.htb/`, added `editorial.htb` to `/etc/hosts`

Found an `/upload` page
![[Pasted image 20240627160338.png]]

via Cover URL, SSRF is possible as we are able to make calls to our external web server
![[Pasted image 20240627160635.png]]

![[Pasted image 20240627160558.png]]

