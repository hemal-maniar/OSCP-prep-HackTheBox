#### nmap

Service scan
```bash
sudo nmap -sC -sV 10.10.10.152 -oA nmap -v
```
![[Pasted image 20241019215855.png]]

#### manual

Despite ProgramData not being visible as a directory via FTP, we can still `cd` into the directory
![[Pasted image 20241019215948.png]]
Under PRTG Configuration.old.bak
![[Pasted image 20241019220025.png]]
Found admin credentials
![[Pasted image 20241019220040.png]]
Found a publicly available [exploit](https://www.exploit-db.com/exploits/46527) for PRTG Network Monitor authenticated RCE
![[Pasted image 20241019220117.png]]


