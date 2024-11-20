##### nmap

All port scan
```bash
sudo nmap -sV -p- -v 10.10.11.193 -oA nmap2 
```
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.52
Service Info: Host: mentorquotes.htb; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Service scan
```bash
sudo nmap -sC -sV 10.10.11.193 -p 22,80 -v -oA nmap
```
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 c7:3b:fc:3c:f9:ce:ee:8b:48:18:d5:d1:af:8e:c2:bb (ECDSA)
|_  256 44:40:08:4c:0e:cb:d4:f1:8e:7e:ed:a8:5c:68:a4:f7 (ED25519)
80/tcp open  http    Apache httpd 2.4.52
| http-methods: 
|_  Supported Methods: GET HEAD OPTIONS
| http-server-header: 
|   Apache/2.4.52 (Ubuntu)
|_  Werkzeug/2.0.3 Python/3.6.9
|_http-title: MentorQuotes
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

UDP Scan
```bash
sudo nmap -sU 10.10.11.193 -vvv
```
```
PORT    STATE         SERVICE REASON
68/udp  open|filtered dhcpc   no-response
161/udp open          snmp    udp-response ttl 63
```
```
PORT    STATE         SERVICE VERSION
68/udp  open|filtered dhcpc
161/udp open          snmp    SNMPv1 server; net-snmp SNMPv3 server (public)
| snmp-info: 
|   enterprise: net-snmp
|   engineIDFormat: unknown
|   engineIDData: a124f60a99b99c6200000000
|   snmpEngineBoots: 67
|_  snmpEngineTime: 1h39m58s
| snmp-sysdescr: Linux mentor 5.15.0-56-generic #62-Ubuntu SMP Tue Nov 22 19:54:14 UTC 2022 x86_64
|_  System uptime: 1h39m58.55s (599855 timeticks)
```
##### manual

- Added mentorquotes.htb to `/etc/hosts`
- snmp port is open

```bash
onesixtyone 10.10.11.193 -c /usr/share/seclists/Discovery/SNMP/snmp-onesixtyone.txt 
```

![[Pasted image 20240904193000.png]]
to
![[Pasted image 20240904193035.png]]

None of this revealed any valuable information

Fuzzing subdomains
```bash
ffuf -u http://10.10.11.193 -H "Host: FUZZ.mentorquotes.htb" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fw 18 -mc all
```
![[Pasted image 20240904195028.png]]

- Added `api.mentorquotes.htb` to `/etc/hosts`

Found out that `internal` community is SNMP is also available as `onesixtyone` only gathers information on v1 but not for v2c and v3. 

- Using snmpbrute.py
![[Pasted image 20240904202819.png]]
- Using `snmpbulkwalk` for much faster enumeration
```bash
snmpbulkwalk -v2c -c internal 10.10.11.193
```
![[Pasted image 20240904203323.png]]

Found a bunch of information but this could be useful
`james:kj23sadkj123as0-d213`

