found `user.txt` in /home/logan but permission denied. This means we need to get logan's credentials

- Found `configuration.php` in /var/www/dev.devvortex.htb/
- it contained the same password for user lewis to connect to mysql DB
- Got logan's hash and cracked it using hashcat
```bash
hashcat -m 3200 logan.hash /usr/share/wordlist/rockyou.txt
```
![[Pasted image 20240905194354.png]]
`logan:tequieromucho`