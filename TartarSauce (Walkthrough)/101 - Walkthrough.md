Found multiple walkthroughs online for privilege escalation

https://0xdf.gitlab.io/2018/10/21/htb-tartarsauce-part-2-backuperer-follow-up.html#root-shell

Privilege escalation is done by creating a 32-bit SUID binary that can later be run when a particular backup script is run on the system and sets SUID bit on the binary allowing us to become root