# ChangeBiosCfg

Updates BIOS settings on the managed system using a configuration file.

## Prerequisites

1. Get current BIOS settings (see GetCurrentBiosCfg)
2. Edit item/variable values in the configuration file
3. Optionally remove unchanged settings/menus

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c ChangeBiosCfg --file <USER_SETUP.file> [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--reboot]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c ChangeBiosCfg --file <USER_SETUP.file> [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--reboot] [--remote_sum <remote sum path>]
```

## Options

- `--file <USER_SETUP.file>`: Required. BIOS configuration file (DAT or XML format)
- `--current_password <current password>`: Current BIOS password (if set)
- `--cur_pw_file <current password file path>`: File containing current BIOS password
- `--reboot`: Reboot system after configuration change
- `--remote_sum <remote sum path>`: Path to remote SUM executable

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBiosCfg --file USER_SETUP.file --reboot
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ChangeBiosCfg --file USER_SETUP.file --reboot
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c ChangeBiosCfg --file USER_SETUP.file --reboot --remote_sum /root/sum
```

## Notes

- Editable BIOS configuration items may vary between BIOS versions
- Configuration changes only take effect after system reboot or power up
- For HII format, re-download configuration after BIOS flash to avoid conflicts
- Use `--skip_unknown` to skip invalid menus/settings when hardware changes
- Use `--skip_bbs` to skip BBS-related menus when boot devices change
- For X11+ platforms, boot device matching uses type and port location
- BIOS configuration XML files use ISO 8859-1 encoding
- Some settings require SFT-DCMS-SINGLE license (SUM 2.5.0+)
