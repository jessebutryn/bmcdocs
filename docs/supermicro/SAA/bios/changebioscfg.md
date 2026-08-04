# ChangeBiosCfg

Updates the BIOS with the given configuration file. Typically used with a USER_SETUP.file obtained from `GetCurrentBiosCfg` or `GetDefaultBiosCfg` and edited to the desired values.

## Prerequisites

1. Get current or default BIOS settings (see `GetCurrentBiosCfg` or `GetDefaultBiosCfg`).
2. Edit the item/variable values in the USER_SETUP.file to the desired values.
3. Optionally remove unchanged settings/menus in the configuration file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeBiosCfg --file <USER_SETUP.file> [--save_as_user_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]]
saa -i <IP or host name> -u <username> -p <password> -c ChangeBiosCfg --save_as_user_default [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]]
```

### In-Band
```
saa -c ChangeBiosCfg --file <USER_SETUP.file> [--save_as_user_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot]
saa -c ChangeBiosCfg --save_as_user_default [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c ChangeBiosCfg --file <USER_SETUP.file> [--save_as_user_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeBiosCfg --file <USER_SETUP.file> [--save_as_user_default] [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]] [--individually]
```

## Options

- `--file <file name>`: Required (unless `--save_as_user_default` is used alone). BIOS configuration file to update the managed system with
- `--save_as_user_default`: Saves the current BIOS configuration as user default
- `--current_password <current password>`: Checks the current BIOS Administrator password
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password
- `--reboot`: Forces the managed system to reboot or power up after operation
- `--individually`: Updates each managed system individually with the corresponding configuration file
- `--skip_unknown`: Skips the unknown settings or menus in the BIOS configuration file
- `--skip_bbs`: Skips the BBS-related menus in the BIOS configuration file
- `--post_complete`: Waits for the managed system's POST to complete after reboot
- `--remote_saa <remote SAA path>`: Path to remote SAA executable (for remote in-band)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBiosCfg --file USER_SETUP.file --reboot
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBiosCfg --file USER_SETUP.file --save_as_user_default --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeBiosCfg --file USER_SETUP.file --reboot
[SAA_HOME]# ./saa -c ChangeBiosCfg --save_as_user_default --reboot
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c ChangeBiosCfg --file USER_SETUP.file --reboot --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeBiosCfg --file USER_SETUP.file --reboot
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeBiosCfg --file USER_SETUP.file --reboot --individually
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c ChangeBiosCfg --file USER_SETUP.file --reboot
```

## Notes

- Editable BIOS configuration items may vary between BIOS versions; ensure the configuration matches the BIOS version on the managed system.
- The uploaded configuration only takes effect after a system reboot or power up.
- When a new BIOS firmware image is flashed, there may be conflicts between the configuration file and the latest BIOS configuration; re-download, re-modify, and re-upload the file.
- When hardware resources or settings change, a previously downloaded configuration file may become outdated. `--skip_unknown` skips all invalid menus and settings; `--skip_bbs` skips all BBS-related menus (menus with "Priorities" in the name and "Boot" as the parent menu).
- SAA matches boot devices by boot type and port location. If SAA can't match the whole boot option string, it tries to match the substring before the first colon (e.g., "UEFI P0: Hard disk A0001" matches "UEFI P0: Hard disk A0002" and "UEFI P0").
- The BIOS configuration XML file contains extended ASCII characters; use ISO 8859-1 encoding.
- A BIOS configuration tagged with `<LicenseRequirement>` requires the SFT-DCMS-SINGLE node product key to change.
- To update multiple systems individually, provide `USER_SETUP.file.<IP>` per system and use `--individually`; SAA searches for `USER_SETUP.file.192.168.34.56` and `USER_SETUP.file.192.168.34.57` to update each respective system.
