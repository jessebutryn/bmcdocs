# MountIsoImage

Mounts an ISO image as virtual media to the managed system through SAMBA/HTTP/HTTPS servers.

## Syntax

```
sum [-i <IP or host name> | [-I Redfish_HI]] [-u <username> -p <password>] -c MountIsoImage --image_url <URL> [[--id <id for URL> --pw <password for URL>] | [--id <id for URL> --pw_file <password file path>]]
```

## Options

- `--image_url <URL>`: URL of the ISO image to mount (supports SAMBA, HTTP, HTTPS, UNC formats).
- `--id <id for URL>`: Username/ID for authentication.
- `--pw <password for URL>`: Password for authentication.
- `--pw_file <password file path>`: File containing the password.

## URL Formats

### HTTP/HTTPS
- `http://<hostname or IP>/<file path>`
- `http://<hostname or IP>:<port>/<file path>`
- `https://<hostname or IP>/<file path>`
- `https://<hostname or IP>:<port>/<file path>`
- IPv6 addresses should be enclosed in square brackets: `[2001:db8::1]`

### SAMBA
- `smb://<hostname or IP>/<file path>`
- `smb://<hostname or IP>:<port>/<file path>`

### UNC
- `\\<hostname or IP>\<file path>`
- `\\<hostname or IP>:<port>\<file path>`

## Examples

### OOB SAMBA
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB SAMBA IPv6
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'smb://[2001:db8::1]/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB HTTP
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'http://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB HTTP IPv6 with port
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'http://[2001:db8::1]:80/MySharedPoint/MyFolder/Image.iso' --id smbid --pw_file smbpasswd.txt
```

### OOB HTTPS
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'https://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB UNC
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url '\\192.168.35.1\MySharedPoint\MyFolder\Image.iso' --id smbid --pw_file smbpasswd.txt
```

### In-Band SAMBA
```
[SUM_HOME]# ./sum -c MountIsoImage --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### In-Band HTTP IPv6
```
[SUM_HOME]# ./sum -c MountIsoImage --image_url 'http://[2001:db8::1]:80/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### In-Band HTTPS
```
[SUM_HOME]# ./sum -c MountIsoImage --image_url 'https://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### In-Band UNC
```
[SUM_HOME]# ./sum -c MountIsoImage --image_url '\\192.168.35.1\MySharedPoint\MyFolder\Image.iso' --id smbid --pw_file smbpasswd.txt
```

## Notes

- Starting from SUM 2.11.0, this command is only supported on platforms that support a single virtual media device only.
- Special characters for ID and password: ^ (caret)
- Special characters for shared host: - (dash) or . (period)
- Special character for HTTP and SAMBA protocols in IPv6 URLs: : (colon)
- Shared host for HTTP IPv6 addresses must be enclosed in square brackets: [ ]
- Special characters for path to image: @,^,-,_,.,/,\
- Special characters like backslashes \ and slashes / should only be used once; repeated use (e.g., //, \\, /\ and \/) is not allowed
- Special character ^ (caret) is not available for use in older versions of BMC firmware
- The port number may not be supported in older versions of BMC firmware
- IPv6 link-local addresses starting with fe80 are not allowed</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/mountisoimage.md