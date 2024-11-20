User `yossi` is physically logged into the host which can be verified using
```bash
w
```
![[Pasted image 20240904165338.png]]

Using [[Find files in groups (no directories)]], we find all files within associated user groups in which one of them stands out
![[Pasted image 20240904172130.png]]

/dev/fb0

- Saved content of `/dev/fb0` into a .raw file `screenshot.raw`
- Viewed the raw file on https://www.photopea.com/
- Loaded `screenshot.raw` file on channel:2 and modified resolution
- The target resolution of the file can be verified 
```bash
cat /sys/class/graphics/fb0/virtual_size
```
![[Pasted image 20240904172427.png]]
![[Pasted image 20240904172444.png]]
Doing this revealed user `yossi`'s password
`MoshePlzStopHackingMe!`