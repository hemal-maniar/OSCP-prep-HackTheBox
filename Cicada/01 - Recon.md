#### nmap

Service scan
```bash
sudo nmap -sC -sV 10.10.11.35 -oA nmap -v 
```
![[Pasted image 20241011182259.png]]
![[Pasted image 20241011182323.png]]
All port scan
```bash
nmap -sV -p- -v 10.10.11.35 -oA nmap2
```
![[Pasted image 20241011183159.png]]
#### manual

![[Pasted image 20241011182605.png]]

Under HR, found a file "Notice from HR.txt"
```
Your default password is: Cicada$M6Corpb*@Lp#nZp!8

To change your password:

1. Log in to your Cicada Corp account** using the provided username and the default password mentioned above.
2. Once logged in, navigate to your account settings or profile settings section.
3. Look for the option to change your password. This will be labeled as "Change Password".
4. Follow the prompts to create a new password**. Make sure your new password is strong, containing a mix of uppercase letters, lowercase letters, numbers, and special characters.
5. After changing your password, make sure to save your changes.

Remember, your password is a crucial aspect of keeping your account secure. Please do not share your password with anyone, and ensure you use a complex password.

If you encounter any issues or need assistance with changing your password, don't hesitate to reach out to our support team at support@cicada.htb.

Thank you for your attention to this matter, and once again, welcome to the Cicada Corp team!

Best regards,
Cicada Corp
```

Added cicada.htb to /etc/hosts

Machine allows guest session that allows us to enumerate users and shares
```bash
nxc smb 10.10.11.35 -u Guest -p '' --rid-brute > user.txt
```

Found a valid user with the above credentials
![[Pasted image 20241012200417.png]]

With the gathered credentials, ldapdomaindumped information to get more data
```bash
ldapdomaindump -u 'cicada.htb\michael.wrightson' -p 'Cicada$M6Corpb*@Lp#nZp!8' --no-json cicada.htb
```
![[Pasted image 20241012202346.png]]

We have credentials of another user `david.orelious:aRt$Lp#7t*VQ!3` 

Using these credentials, gained access to DEV share which contains Backup_script.ps1
![[Pasted image 20241012202801.png]]
We now have user `emily.oscars:Q!3@Lp#M6b*7t*Vt`

From ldapdomaindump, we know that user `emily.oscars` has remote management access and is also a member of backup operators group
![[Pasted image 20241012202906.png]]
