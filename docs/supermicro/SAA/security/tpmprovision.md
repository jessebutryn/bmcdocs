# TpmProvision

Enables or clears TPM module capabilities for the managed system using a TPM ISO image on platforms before X11 Intel Xeon Scalable Processors with Intel C620 Series Chipsets (from the X10 Intel Xeon Processor E5 v3/v4 Product Family through the X11 Intel Xeon Scalable Processors with Intel C620 Series Chipsets). OOB use only. The TPM module must be installed on the managed system before executing this command.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c TpmProvision --image_url <URL> --reboot --lock <yes> [[--id <id for URL> --pw <password for URL>] | [--id <id for URL> --pw_file <password file path>]]
```

### Multiple Systems OOB
```
saa -l <system list file> -u <username> -p <password> -c TpmProvision --image_url <URL> --reboot --lock <yes> [[--id <id for URL> --pw <password for URL>] | [--id <id for URL> --pw_file <password file path>]]
```

### Clearing TPM Capabilities (OOB)
```
saa -i <IP or host name> -u <username> -p <password> -c TpmProvision --image_url <URL> [--id <id for URL> --pw <password for URL>] --cleartpm --reboot
```

### Clearing TPM Capabilities (Multiple Systems OOB)
```
saa -l <system list file> [-u <username> -p <password>] -c TpmProvision --image_url <URL> [--id <id for URL> --pw <password for URL>] --cleartpm --reboot
```

## Options

- `--reboot`: Forces the managed system to reboot or power up after operation
- `--image_url <URL>`: The URL to access the shared TPM ISO image file. Supported formats:
    - SAMBA URL: `smb://<host name or ip>/<shared point>/<file path>`
    - SAMBA UNC: `\<host name or ip>\<shared point>\<file path>`
    - HTTP URL: `http://<host name or ip>/<shared point>/<file path>`
- `--lock <yes>`: Locks the TPM module
- `--id <ID>`: (Optional) Allows the specified ID to access the shared file
- `--pw <Password>`: (Optional) The specified password to access the shared file
- `--pw_file <Password File>`: (Optional) The specified file path to read the password
- `--cleartpm`: (Optional) Clears the ownership of the TPM module and restores the relevant TPM BIOS settings

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmProvision --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder' --id smbid --pw smbpasswd --reboot --lock yes

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmProvision --image_url 'http://192.168.35.1/MySharedPoint/MyFolder' --id smbid --pw smbpasswd --reboot --lock yes

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmProvision --image_url '\192.168.35.1\MySharedPoint\MyFolder' --id smbid --pw_file smbpasswd.txt --reboot --lock yes
```

`smbpasswd.txt`:
```
smbpasswd
```

### Clearing TPM Capabilities (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmProvision --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder' --id smbid --pw smbpasswd --cleartpm --reboot
```

### Clearing TPM Capabilities (Multiple Systems OOB)
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c TpmProvision --image_url 'smb://192.168.35.1/MySharedPoint/MyFolder' --id smbid --pw smbpasswd --cleartpm --reboot
```

## Notes

- This command is supported from the X10 Intel Xeon Processor E5 v3/v4 Product Family through the X11 Intel Xeon Scalable Processors with Intel C620 Series Chipsets platforms.
- The TPM ISO images are not included in the SAA package and must be acquired from Supermicro. Each SAA release may require a different ISO image, as noted in the SAA release notes. Acquire the correct `TPM_version_YYYYMMDD.zip`, unzip it, and use the TPM ISO images contained within.
- With the TPM ISO images, TPM capabilities can be enabled or cleared. The BIOS reboots several times during provisioning.
- Space is prohibited in a SAMBA password.
- SAA checks the TPM module status on the managed system; if it is not installed or has malfunctioned, exit code 36/37 is returned respectively. If the TPM is locked, exit code 37 is returned.
- The `--cleartpm` option clears the ownership of the TPM module.
- The `--lock yes` option locks the TPM module.
- SAA stops the TPM provisioning procedure if the CPU or platform does not support Intel Trusted Execution Technology (Intel TXT).
- On platforms after X11 Intel Xeon Scalable Processors with Intel C620 Series Chipsets, use `TpmManage` instead.
