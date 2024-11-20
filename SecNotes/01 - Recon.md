##### nmap

All port scan
```bash
sudo nmap -sV -p- 10.10.10.97 -v -oA nmap2
```
```
PORT     STATE SERVICE      VERSION
80/tcp   open  http         Microsoft IIS httpd 10.0
445/tcp  open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: HTB)
8808/tcp open  http         Microsoft IIS httpd 10.0
Service Info: Host: SECNOTES; OS: Windows; CPE: cpe:/o:microsoft:windows
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.97 -p 80,445,8808 -v -oA nmap
```
```
PORT     STATE SERVICE      VERSION
80/tcp   open  http         Microsoft IIS httpd 10.0
| http-title: Secure Notes - Login
|_Requested resource was login.php
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
445/tcp  open  microsoft-ds Windows 10 Enterprise 17134 microsoft-ds (workgroup: HTB)
8808/tcp open  http         Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows
Service Info: Host: SECNOTES; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2024-09-06T14:05:07
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 10 Enterprise 17134 (Windows 10 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: SECNOTES
|   NetBIOS computer name: SECNOTES\x00
|   Workgroup: HTB\x00
|_  System time: 2024-09-06T07:05:09-07:00
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 2h20m01s, deviation: 4h02m31s, median: 0s
```

##### manual

- Can not log into SMB share anonymously. Moving over to webservers
![[Pasted image 20240906180536.png]]
- Going over to http://10.10.10.97 was a login page. It also contains the capability of creating a user
```
username: hacker
password: hacker
```
- Logged in using the created user 
![[Pasted image 20240906180743.png]]
- We have a potential user on system
![[Pasted image 20240906180756.png]]
- Added secnotes.htb to /etc/hosts

Found out that the website is vulnerable to XSS but did not get anything down that path. Also attempted to make a [JSshell](https://github.com/Den1al/JSShell) script that can be captured if user `tyler` opens the message through "Contact Us" form. This did not work either but we are assuming that user tyler opens messages via the form. 

Using the `change_pass.php` form, there's a CSRF where changing the method from POST to GET and moving the parameters into the URL
![[Pasted image 20240907111143.png]]
![[Pasted image 20240907111208.png]]
Sent this link over in contact form
http://secnotes.htb//change_pass.php?password=hacker3&confirm_password=hacker3&submit=submit
This instantly is changes tyler's password to hacker3

- Found a note by `tyler` titled "new site"
![[Pasted image 20240907111341.png]]
`tyler:92g!mA8BGjOirkL%OG*&`
![[Pasted image 20240907111415.png]]

![[Pasted image 20240907111501.png]]
The SMB share looks like website directory of webserver running on port 8808