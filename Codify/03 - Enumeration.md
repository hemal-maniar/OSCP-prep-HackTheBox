- As user `joshua`, running 
```bash
sudo -l
```
![[Pasted image 20240902223940.png]]

We can run the `mysql-backup.sh` script as root. The script verifies a password that is validated before running the backup script. 

An incorrect password is shown
![[Pasted image 20240902224214.png]]

The password check can be bypassed by using `*` 
![[Pasted image 20240902224200.png]]

