# LoadDefaultBiosCfg

Resets the BIOS settings of the managed system to the factory default settings.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c LoadDefaultBiosCfg [--optimized_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]] [--redfish]
saa -i <IP or host name> -u <username> -p <password> -c LoadDefaultBiosCfg --show
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c LoadDefaultBiosCfg [--optimized_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot] [--redfish]
saa -c LoadDefaultBiosCfg --show
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c LoadDefaultBiosCfg [--optimized_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot] [--remote_saa <remote SAA path>] [--redfish]
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c LoadDefaultBiosCfg --show
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c LoadDefaultBiosCfg [--optimized_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]] [--redfish]
saa -l <system list file> [-u <username> -p <password>] -c LoadDefaultBiosCfg --show
```

## Options

- `--optimized_default`: Restores the BIOS to default settings with optimization
- `--current_password <current password>`: Checks the current BIOS Administrator password
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password
- `--reboot`: Forces the managed system to reboot or power up after operation
- `--redfish`: Enables support for pure Redfish
- `--post_complete`: Waits for the managed system's POST to complete after reboot
- `--clear_bios_eventlog`: Clears the BIOS event log
- `--show`: Shows the BIOS current default status

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBiosCfg --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -c LoadDefaultBiosCfg --show
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c LoadDefaultBiosCfg --reboot --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LoadDefaultBiosCfg --optimized_default --reboot
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c LoadDefaultBiosCfg --reboot
```

## Output

### With --show
```
Managed system......................localhost
 BIOS default....................Optimized Default
```

## Notes

- The uploaded configuration only takes effect after a reboot or power up.
- If you don't use `--optimized_default`, the managed system is restored to its current default setting, which may be the user-selected default or the performance-optimized default. For platforms that do not support `--optimized_default`, the current default setting is the performance-optimized setting.
