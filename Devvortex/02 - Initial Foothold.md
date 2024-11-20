There's a way to gain RCE from admin panel as provided in [HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/joomla#rce)
- Edited `error.php` located in ![[Pasted image 20240905193359.png]]
- and replaced the code with a php reverse shell
- call the script using `curl`
```bash
curl -s http://dev.devvortex.htb/templates/cassiopeia/cassiopeia/error.php
```
Got shell as `www-data`

