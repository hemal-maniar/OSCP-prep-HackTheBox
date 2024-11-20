##### nmap

All port scan
```bash
sudo nmap -sV -p- 10.10.10.11 -v -oA nmap2
```
```
PORT      STATE SERVICE VERSION
135/tcp   open  msrpc   Microsoft Windows RPC
8500/tcp  open  fmtp?
49154/tcp open  msrpc   Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

##### manual 

- Navigating manually to http://10.10.10.11:8500, and it seems directory listing seems to be enabled 
![[Pasted image 20240910103328.png]]
and it is being run on JRun Web Server
![[Pasted image 20240910103407.png]]

- http://10.10.10.11:8500/cfdocs
![[Pasted image 20240910103503.png]]
- Adobe Coldfusion 8 is running on the system
![[Pasted image 20240910103520.png]]
- A quick search on [exploitDB](https://www.exploit-db.com/exploits/50057) gives a publicly available RCE for Adobe ColdFusion 8 