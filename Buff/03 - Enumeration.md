```powershell
Get-ChildItem -Directory -Recurse | Where-Object { (Get-ChildItem $_.FullName -File).Count -gt 0 } | ForEach-Object { Write-Output "Contents of $($_.FullName):"; Get-ChildItem $_.FullName }
```

enumerated all directories for files under C:\\Users. We have some files that could be important
![[Pasted image 20240908121329.png]]
- Tasks.bat
![[Pasted image 20240908121409.png]]
