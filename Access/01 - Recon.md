##### nmap

All port scan
```bash
sudo nmap -sV -p- 10.10.10.98 -v -oA nmap2
```
```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
23/tcp open  telnet?
80/tcp open  http    Microsoft IIS httpd 7.5
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.98 -p 21,23,80 -v -oA nmap   
```
```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     Microsoft ftpd
| ftp-syst: 
|_  SYST: Windows_NT
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 425 Cannot open data connection.
23/tcp open  telnet?
80/tcp open  http    Microsoft IIS httpd 7.5
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-title: MegaCorp
|_http-server-header: Microsoft-IIS/7.5
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

##### manual

- we know that anonymous login is allowed, as mentioned in the nmap scan
- logged in as anonymous
```bash
ftp 10.10.10.95 
```
![[Pasted image 20240906155735.png]]
- successfully logged into the FTP server
- ![[Pasted image 20240906155757.png]]
- There's 2 directories: /Backups, /Engineer
- Backups contains backup.mdb file
- Engineer contains "Access Control.zip"
- Attempted to download the 2 files from 2 folders but
![[Pasted image 20240906155904.png]]
- It seems we're not getting the complete file
- In FTP, switched to binary and downloaded the files
![[Pasted image 20240906155942.png]]
- This worked without any issues 

`backup.mdb` is a Windows Access Management DB file so transferred the file over to Windows machine and viewed it in Microsoft Access
![[Pasted image 20240906160042.png]]
Found a table `auth_user` containing some usernames and credentials

`Access Control.zip` contains a .pst (an Outlook database file) that is password protected. Used password `access4u@security` as the password to extract this file. 

In Microsoft Outlook, opened the file using **File > Open & Export > Open Outlook Data File** and selected `Access Control.pst` file.  

The .pst file contains 1 email
![[Pasted image 20240906160257.png]]
It says that password for security account has been changed to `4Cc3ssC0ntr0ller`
