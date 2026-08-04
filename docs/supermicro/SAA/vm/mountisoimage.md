# MountIsoImage

Mounts an ISO image as virtual media to the managed system through a SAMBA/HTTP/HTTPS server. This command is only supported on platforms that support a single virtual media device.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c MountIsoImage --image_url <URL> [[--id <id for URL> --pw <password for URL>] | [--id <id for URL> --pw_file <password file path>]]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c MountIsoImage --image_url <URL> [[--id <id for URL> --pw <password for URL>] | [--id <id for URL> --pw_file <password file path>]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c MountIsoImage --image_url <URL> [[--id <id for URL> --pw <password for URL>] | [--id <id for URL> --pw_file <password file path>]]
```

## Options

- `--image_url <URL>`: The URL to access the shared image file. Supports SAMBA URL (`smb://<host name or ip>/<shared point>/<file path>`), SAMBA UNC, and HTTP URL (`http://<host name or ip>/<shared point>/<file path>`) formats.
- `--id <ID>` (Optional): The specified ID to access the shared file.
- `--pw <Password>` (Optional): The specified password to access the shared file.
- `--pw_file <Password File>` (Optional): The specified file path to read the password.
- `--redfish` (Optional): Enables support for pure Redfish.

## Examples

### OOB SAMBA
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB SAMBA IPv6
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'smb://[2001:db8::1]/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB HTTP
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'http://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB HTTP IPv6 with Port
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'http://[2001:db8::1]:80/MySharedPoint/MyFolder/Image.iso' --id smbid --pw_file smbpasswd.txt
```

### OOB HTTPS
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'https://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### OOB UNC
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountIsoImage --image_url '\192.168.35.1\MySharedPoint\MyFolder\Image.iso' --id smbid --pw_file smbpasswd.txt
```

### In-Band SAMBA
```bash
[SAA_HOME]# ./saa -c MountIsoImage --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### In-Band HTTPS
```bash
[SAA_HOME]# ./saa -c MountIsoImage --image_url 'https://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c MountIsoImage --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

If the execution "Status" field for a managed system is SUCCESS, the ISO image is mounted as a virtual media to the managed system.

## Notes

- This command is only supported on platforms that support a single virtual media device. For platforms that support multiple virtual media devices, use `VmManage` with `--action Mount` instead.
- Allowed character classes: a-z, A-Z, 0-9.
- Special characters for ID and password: `^` (caret).
- Special characters for a shared host: `-` (dash) or `.` (period).
- Special character for a shared host in HTTP and SAMBA protocols in an IPv6 URL: `:` (colon). The shared host for an HTTP IPv6 address should be enclosed in square brackets `[ ]`.
- Special characters for path to image: `@`, `^`, `-`, `_`, `.`, `/`, and `\` (`/` and `\` can only be used in a path).
- Special characters like backslashes `\` and slashes `/` should only be used once; repeated use (e.g., `//`, `\\`, `/\` and `\/`) is not allowed.
- Special character `^` (caret) is not available for use in older versions of BMC firmware.
- The port number may not be supported in older versions of BMC firmware.
- An IPv6 link-local address starting with `fe80` is not allowed.
