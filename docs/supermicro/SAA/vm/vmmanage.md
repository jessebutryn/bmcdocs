# VmManage

Manages virtual media on the managed system. Use the `Enable`/`Disable` actions to control virtual media status on all platforms that support virtual media management. On platforms that support multiple virtual media devices, use the `Mount`/`Unmount` actions to mount or unmount an image on a specific virtual media device. This command supports up to three virtual media devices, including ISO and floppy images.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c VmManage --action <Enable|Disable> [--port <port>]

saa -i <IP or host name> -u <username> -p <password> -c VmManage --action Mount [--dev_id <device ID>] --image_url <URL> [[--id <id for URL> --pw <password for URL>]|[--id <id for URL> --pw_file <password file path>]] [--verify_cert [--accept_self_signed]]

saa -i <IP or host name> -u <username> -p <password> -c VmManage --action Unmount [--dev_id <device ID>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c VmManage --action <Enable|Disable> [--port <port>]

saa -I Redfish_HI -u <username> -p <password> -c VmManage --action Mount [--dev_id <device ID>] --image_url <URL> [[--id <id for URL> --pw <password for URL>]|[--id <id for URL> --pw_file <password file path>]] [--verify_cert [--accept_self_signed]]

saa -I Redfish_HI -u <username> -p <password> -c VmManage --action Unmount [--dev_id <device ID>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c VmManage --action <Enable|Disable> [--port <port>]

saa -l <system list file> [-u <username> -p <password>] -c VmManage --action Mount [--dev_id <device ID>] --image_url <URL> [[--id <id for URL> --pw <password for URL>]|[--id <id for URL> --pw_file <password file path>]] [--verify_cert [--accept_self_signed]]

saa -l <system list file> [-u <username> -p <password>] -c VmManage --action Unmount [--dev_id <device ID>]
```

## Actions

- **Enable/Disable** (`--action 1`/`2`): Enables or disables virtual media from the BMC. The `--port` option is optional; if provided, SAA configures the virtual media port of the BMC.
- **Mount** (`--action 3`): Mounts an image from the image file server to the specified virtual media device of the BMC. Requires `--image_url`; optionally `--id`, `--pw`/`--pw_file`, `--dev_id`, `--verify_cert`, and `--accept_self_signed`.
- **Unmount** (`--action 4`): Unmounts the image from the specified virtual media device of the BMC. Use `--dev_id` to specify the device, or `--dev_id ALL` to unmount all devices.

## Options

- `--action <action>`: Sets action to 1 = Enable, 2 = Disable, 3 = Mount, 4 = Unmount.
- `--port <port>` (Optional): Command optional port(s). The format is "VM:623" or "623." Supported port: VM (virtual media port).
- `--image_url <URL>`: The URL to access the shared image file. Supports SAMBA URL (`smb://<host name or ip>/<shared point>/<file path>`), SAMBA UNC, and HTTP URL (`http://<host name or ip>/<shared point>/<file path>`) formats.
- `--id <ID>` (Optional): The specified ID to access the shared file.
- `--pw <Password>` (Optional): The specified password to access the shared file.
- `--pw_file <Password File>` (Optional): The specified file path to read the password.
- `--dev_id <Device ID>` (Optional): The specified device ID to manage a virtual media device. The supported device ID: [1-3]. Supports "ALL" for the Unmount action to unmount all devices.
- `--verify_cert` (Optional): Verifies the SSL certificate. Only supported for the HTTPS protocol.
- `--accept_self_signed` (Optional): Accepts the self-signed certificate. Only supported for the HTTPS protocol.

## Examples

### Enable/Disable (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c VmManage --action Enable --port 623
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c VmManage --action Disable --port 623
```

### Mount (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c VmManage --action Mount --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd --dev_id 1

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c VmManage --action Mount --image_url 'https://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd --verify_cert --accept_self_signed --dev_id 2
```

### Unmount (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c VmManage --action Unmount --dev_id 1
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c VmManage --action Unmount --dev_id ALL
```

`smbpasswd.txt`:
```
smbpasswd
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c VmManage --action Enable --port 623
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c VmManage --action Mount --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd --dev_id 1
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c VmManage --action Unmount --dev_id 1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c VmManage --action Enable --port 623
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c VmManage --action Mount --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder/Image.iso' --id smbid --pw smbpasswd --dev_id 1
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c VmManage --action Unmount --dev_id ALL
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.

## Notes

- On platforms that only support a single virtual media device, use `MountIsoImage`, `UnmountIsoImage`, `MountFloppyImage`, and `UnmountFloppyImage` instead of the Mount/Unmount actions.
- The `--port` option is optional for the Enable/Disable action.
- Special characters for ID and password: `^` (caret).
- Special characters for shared host: `-` (dash) or `.` (period).
- Special character for HTTP and SAMBA protocols in an IPv6-format URL shared host: `:` (colon). The shared host for the HTTP protocol in IPv6 format must be enclosed with square brackets `[ ]`.
- Special characters for path to image: `@^-_./\` (`/` and `\` can only be used in a path).
- Special characters like backslashes `\` and slashes `/` should only be used once; repeated use (e.g., `//`, `\\`, `/\` and `\/`) is not allowed.
- Special character `^` (caret) is not available for use in older versions of BMC firmware.
- The port number may not be supported in older versions of BMC firmware.
- An IPv6 link-local address starting with `fe80` is not allowed.
- Up to three virtual media devices are supported, including ISO and floppy images.
- If a device is mounted by iKVM, it can only be unmounted by iKVM.
