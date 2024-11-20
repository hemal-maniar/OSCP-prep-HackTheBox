Was able to successfully SSH as `sunny:sunday`

- Found that `user.txt` file is in sammy's home folder that can not be read
- Found a `backup` folder in / directory containing a shadow file backup 
- Saved user `sammy`'s hash and attempted to crack it using john
- Cracking password
```bash
john sammy.hash --wordlist=/usr/share/wordlists/rockyou.txt
```
![[Pasted image 20240902145417.png]]

Logging in as user `sammy:cooldude!`
