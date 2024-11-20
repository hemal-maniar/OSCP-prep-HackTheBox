Ran linpeas.sh and found an interesting group that the user `ash` is added to which is `116(lxd)`

Found a guide to privesc using an [LXD alpine container](https://juggernaut-sec.com/lxd-container/)

Followed the steps which ended up mounting the entire filesystem onto `/mnt/root` within the container allowing us to view contents of /root folder revealing the flag

NOTE: make sure to initialize LXD
```bash
lxd init
```