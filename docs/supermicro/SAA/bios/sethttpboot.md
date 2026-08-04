# SetHttpBoot

Downloads an ISO image from an HTTP or HTTPS server and boots from it.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetHttpBoot [--current_password <current password> | --cur_pw_file <current password file path>] [--boot_lan <boot lan port>] [--boot_name <boot description>] --image_url <URL> [--reboot [--post_complete]] [--file <file name>]
saa -i <IP or host name> -u <username> -p <password> -c SetHttpBoot --boot_clean [--reboot [--post_complete]]
```

### In-Band
```
saa -c SetHttpBoot [--current_password <current password> | --cur_pw_file <current password file path>] [--boot_lan <boot lan port>] [--boot_name <boot description>] --image_url <URL> [--reboot] [--file <file name>]
saa -c SetHttpBoot --boot_clean [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetHttpBoot [--current_password <current password> | --cur_pw_file <current password file path>] [--boot_lan <boot lan port>] [--boot_name <boot description>] --image_url <URL> [--reboot [--post_complete]] [--file <file name>]
saa -l <system list file> [-u <username> -p <password>] -c SetHttpBoot --boot_clean [--reboot [--post_complete]]
```

## Options

- `--current_password <current password>`: Checks the current BIOS Administrator password
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password
- `--file <file name>`: Uploads the TLS certificate, in the formats `.cer`, `.der`, `.crt`, or `.pem`
- `--boot_name <boot description>`: Description for HTTP boot
- `--boot_lan <boot lan port>`: Enters the LAN port for HTTP boot
- `--reboot`: Forces the managed system to reboot or power up after operation
- `--boot_clean`: Cleans all HTTP boot options
- `--disable_hostname_check`: Disables checking whether the host name of the TLS certificate matches the host name provided by the remote server for HTTPS boot
- `--image_url <URL>`: The URL to access the shared image file, in the format `http://<IPv4 or IPv6>/<shared point>/<file path>` or `https://<IPv4 or IPv6>/<shared point>/<file path>`
- `--post_complete`: Waits for the managed system's POST to complete after reboot

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetHttpBoot --boot_name bootDescription --image_url http://192.168.12.78/iso/efishell.iso --reboot
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetHttpBoot --boot_lan 2 --boot_name bootDescription --file TLS.crt --image_url https://[1234:ab5:0:c678:9012:345d:6e78:9f0a]/iso/efishell.iso --reboot
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetHttpBoot --boot_clean --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SetHttpBoot --boot_name bootDescription --image_url http://192.168.12.78/iso/efishell.iso --reboot
[SAA_HOME]# ./saa -c SetHttpBoot --boot_lan 2 --boot_name bootDescription --file TLS.crt --image_url https://[1234:ab5:0:c678:9012:345d:6e78:9f0a]/iso/efishell.iso --reboot
[SAA_HOME]# ./saa -c SetHttpBoot --boot_clean --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetHttpBoot --boot_name bootDescription --image_url http://192.168.12.78/iso/efishell.iso --reboot
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetHttpBoot --boot_lan 2 --boot_name bootDescription --file TLS.crt --image_url https://[1234:ab5:0:c678:9012:345d:6e78:9f0a]/iso/efishell.iso --reboot
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetHttpBoot --boot_clean --reboot
```

## Notes

- HTTPS boot needs to provide clients with a valid TLS certificate signed by a trusted Certification Authority.
- Due to BIOS limitations, if an HTTP boot option already exists in the BIOS configuration, use `--boot_clean` to clean the HTTP boot option and then reset the HTTP boot option.
- On FreeBSD 12, executing this command may boot into FreeBSD instead of `efishell.iso` because of `startup.nsh` in the system; delete or rename the `startup.nsh` file to prevent this.
- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
