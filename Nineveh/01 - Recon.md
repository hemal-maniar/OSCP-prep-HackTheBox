#### nmap
```bash
sudo nmap -sC -sV 10.10.10.43 -oA nmap -v
```
![[Pasted image 20241013171939.png]]

All port scan
```bash
nmap -sV -p- -v 10.10.10.43 -Pn
```

Navigated to the website and on port 80, found a web directory `/department` that redirects to login.php. On the webpage, there's a comment
![[Pasted image 20241013173041.png]]
