#### nmap

All port scan
```bash
sudo nmap -sC -sV 10.10.11.108 -oA nmap -v
```
![[Pasted image 20241012223201.png]]

All port scan
```bash
nmap -sV -p- -v 10.10.11.108 -Pn
```

#### manual

![[Pasted image 20241013120202.png]]
Observing the POST request on submitting "Update"
![[Pasted image 20241013120252.png]]

Starting listener
![[Pasted image 20241013120340.png]]
and modifying POST request
![[Pasted image 20241013120425.png]]
Got user `svc-printer` password 
![[Pasted image 20241013124147.png]]
