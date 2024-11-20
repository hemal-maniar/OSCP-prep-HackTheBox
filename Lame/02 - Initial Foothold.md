Found a public exploit for CVE-2004-2687 on [GitHub](https://github.com/angelpimentell/distcc_cve_2004-2687_exploit) that allows RCE by exploiting DistCC daemon 
![[Pasted image 20240831160921.png]]
here we can see the root directory for user `daemon` is in the /tmp folder which is accessible via the SMB share
