- Under `/var/www/htmlfiles`, found a backup.zip file that I transferred over to Kali
- Extract zip hash
```bash
zip2john 16162020_backup.zip > 16162020_backup.hash
```
- Crack hash
```bash
john 16162020_backup.hash --wordlist=/usr/share/wordlists/rockyou.txt 
```
- Cracked the password of zip file to be `admin@it`
![[Pasted image 20240903221035.png]]
