##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.10.95 -oA nmap2
```
```
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
```

Service scan
```bash
sudo nmap -sC -sV 10.10.10.95 -p 8080 -v -oA nmap
```
```
PORT     STATE SERVICE VERSION
8080/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-favicon: Apache Tomcat
|_http-title: Apache Tomcat/7.0.88
|_http-server-header: Apache-Coyote/1.1
```

Found an RCE for Apache Tomcate/Coyote JSP 1.1 [CVE-2017-12615]
That did not work

Tried some default passwords on http://10.10.10.95:8080/manager/status and `tomcat:tomcat` worked 