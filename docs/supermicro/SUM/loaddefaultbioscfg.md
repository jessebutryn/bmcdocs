# LoadDefaultBiosCfg

Resets the BIOS settings of the managed system to factory default settings.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c LoadDefaultBiosCfg [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--reboot]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c LoadDefaultBiosCfg [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--reboot] [--remote_sum <remote sum path>]
```

## Options

- `--current_password <current password>`: Current BIOS password (if set).
- `--cur_pw_file <current password file path>`: File containing the current BIOS password.
- `--reboot`: Forces the managed system to reboot after loading default settings.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBiosCfg --reboot
```

### In-Band
```
[SUM_HOME]# ./sum -c LoadDefaultBiosCfg --reboot
```

### Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c LoadDefaultBiosCfg --reboot --remote_sum /root/sum
```

## Notes

- The uploaded configuration will take effect only after a reboot or power up.
- If a BIOS password is set, you may need to provide the current password.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/loaddefaultbioscfg.md