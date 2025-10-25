# SetHttpBoot

Downloads an ISO image from an HTTP server and boots into the ISO image.

## Syntax

### Set HTTP Boot
```
sum [-i <IP or host name> -u <username> -p <password>] -c SetHttpBoot [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--boot_lan <boot lan port>] [--boot_name <boot description>] --image_url <URL> [--reboot] [--file <file name>]
```

### Clean HTTP Boot
```
sum [-i <IP or host name> -u <username> -p <password>] -c SetHttpBoot --boot_clean [--reboot]
```

## Options

- `--current_password <current password>`: Current password for authentication.
- `--cur_pw_file <current password file path>`: File containing the current password.
- `--boot_lan <boot lan port>`: Specifies the boot LAN port.
- `--boot_name <boot description>`: Description for the boot entry.
- `--image_url <URL>`: URL of the ISO image to download.
- `--reboot`: Forces the managed system to reboot after setting up HTTP boot.
- `--file <file name>`: TLS certificate file for HTTPS boot.
- `--boot_clean`: Cleans the HTTP boot option.

## Examples

### OOB HTTP Boot
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetHttpBoot --boot_name bootDescription --image_url http://192.168.12.78/iso/efishell.iso --reboot
```

### OOB HTTPS Boot with Certificate
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetHttpBoot --boot_lan 2 --boot_name bootDescription --file TLS.crt --image_url https://[1234:ab5:0:c678:9012:345d:6e78:9f0a]/iso/efishell.iso --reboot
```

### OOB Clean HTTP Boot
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetHttpBoot --boot_clean --reboot
```

### In-Band HTTP Boot
```
[SUM_HOME]# ./sum SetHttpBoot --boot_name bootDescription --image_url http://192.168.12.78/iso/efishell.iso --reboot
```

### In-Band HTTPS Boot with Certificate
```
[SUM_HOME]# ./sum -c SetHttpBoot --boot_lan 2 --boot_name bootDescription --file TLS.crt --image_url https://[1234:ab5:0:c678:9012:345d:6e78:9f0a]/iso/efishell.iso --reboot
```

### In-Band Clean HTTP Boot
```
[SUM_HOME]# ./sum -c SetHttpBoot --boot_clean --reboot
```

## Notes

- HTTPS boot needs to provide the clients with a valid TLS certificate signed by a trusted Certificate Authority.
- Due to BIOS limitations, if an HTTP boot option exists in the BIOS configuration, please use the --boot_clean option to clean the HTTP boot option and then reset HTTP the boot option.
- When you execute the SetHttpBoot command on the FreeBSD 12 system, you may boot into FreeBSD instead of efishell.iso because of startup.nsh in the system. To prevent from it, you can delete startup.nsh or rename the startup.nsh file.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/sethttpboot.md