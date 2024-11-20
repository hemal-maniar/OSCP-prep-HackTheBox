##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.11.239 -oA nmap2
```
```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    Apache httpd 2.4.52
3000/tcp open  http    Node.js Express framework
```

Service scan
```bash
sudo nmap -sC -sV 10.10.11.239 -p 22,80,3000 -v -oA nmap
```
```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 96:07:1c:c6:77:3e:07:a0:cc:6f:24:19:74:4d:57:0b (ECDSA)
|_  256 0b:a4:c0:cf:e2:3b:95:ae:f6:f5:df:7d:0c:88:d6:ce (ED25519)
80/tcp   open  http    Apache httpd 2.4.52
|_http-title: Codify
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.52 (Ubuntu)
3000/tcp open  http    Node.js Express framework
|_http-title: Codify
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel```

##### nikto 

```bash
nikto -h http://10.10.11.239
```
```
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.10.11.239
+ Target Hostname:    10.10.11.239
+ Target Port:        80
+ Start Time:         2024-09-02 15:32:34 (GMT4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.52 (Ubuntu)
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ Root page / redirects to: http://codify.htb/
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.4.52 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ 8074 requests: 0 error(s) and 3 item(s) reported on remote host
+ End Time:           2024-09-02 15:49:49 (GMT4) (1035 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

- Added codify.htb to `/etc/hosts`
- /about
![[Pasted image 20240902174145.png]]
- Found a sandbox escape vulnerability in vm2 on [ExploitDB](https://www.exploit-db.com/exploits/51898)
- ran that code in /editor
![[Pasted image 20240902174238.png]]