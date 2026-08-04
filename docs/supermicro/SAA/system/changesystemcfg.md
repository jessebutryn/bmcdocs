# ChangeSystemCfg

Updates the managed system with the given configuration file. Typical usage is to first get the current settings with `GetSystemCfg`, edit the configurable element values in the resulting `SystemCfg.xml` file, then apply the updated file with `ChangeSystemCfg`.

## Syntax

### OOB
```
saa -i <BMC IP or host name> -u <username> -p <password> -c ChangeSystemCfg --file <SystemCfg.xml> [--reboot [--post_complete]]
saa -i <CMM IP or host name> -u <username> -p <password> -c ChangeSystemCfg [[--update Apply|Deploy --dev_id <Device ID> --file_id <file ID> --reboot] | [--upload --file SystemCfg.xml]]
```

### In-Band
```
saa -c ChangeSystemCfg --file <SystemCfg.xml> [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeSystemCfg --file <SystemCfg.xml> [--reboot [--post_complete]]
saa -l <system list file> [-u <username> -p <password>] -c ChangeSystemCfg [[--update Apply|Deploy --dev_id <Device ID> --file_id <file ID> --reboot] | [--upload --file SystemCfg.xml]]
```

## Options

- `--file <file name>`: Updates the managed system with the given configuration file.
- `--current_password <current password>`: Checks the current BIOS Administrator password.
- `--upload`: Uploads the Blade system configuration file to the CMM for updating a profile.
- `--file_id <file ID>`: Assigns the profile ID using the `ProfileManage` command.
- `--update <update rule>`: Updates the Blade system configuration with the existing system profile on the CMM. Supported update rules: `Apply` or `Deploy`.
- `--skip_precheck`: (Optional) Uploads and overwrites the existing CMM profile.
- `--reboot`: Forces the managed system to reboot or power up after the operation.
- `--dev_id <Device ID>`: Assigns Blade index and node ID. Blade index: `[A1-A14]` or `[B1-B14]`; Node ID: `[1-4]`; format: `A1`, `A1_1`, or `ALL` for all blade nodes.
- `--skip_unknown`: Skips unknown settings or menus in the system configuration file.
- `--skip_bbs`: Skips the BBS-related menus in the BIOS configuration file.
- `--precheck`: Checks the configuration before the update.
- `--post_complete`: Waits for the managed system to complete POST after rebooting.
- `--cur_pw_file <Current password file>`: The specified file path to read the BIOS Administrator password.
- `--individually`: Searches for per-system configuration files (e.g. `SystemCfg.xml.192.168.34.56`) to update each managed system in a system list individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeSystemCfg --file SystemCfg.xml

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeSystemCfg --upload --file SystemCfg.xml

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeSystemCfg --update Apply --dev_id A1_1,B11_2,A10 --file_id 2 --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeSystemCfg --update Apply --dev_id ALL --file_id 2 --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeSystemCfg --file SystemCfg.xml

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeSystemCfg --file SystemCfg.xml --individually

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeSystemCfg --upload --file SystemCfg.xml

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeSystemCfg --update Apply --dev_id A1_1,B11_2,A10 --file_id 2 --reboot

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeSystemCfg --update Apply --dev_id ALL --file_id 2 --reboot
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the Status field of a managed system shows SUCCESS, its system settings are updated.

To update both 192.168.34.56 and 192.168.34.57, provide two files, `SystemCfg.xml.192.168.34.56` and `SystemCfg.xml.192.168.34.57`, and pass `--file SystemCfg.xml`. With the `--individually` option, SAA searches for `SystemCfg.xml.192.168.34.56` and `SystemCfg.xml.192.168.34.57` to update 192.168.34.56 and 192.168.34.57 respectively.

## Notes

- The connection might be lost if the LAN configuration is changed.
- You can use `--upload` to change the CMM configuration, then use the `GetCmmCfg` command with `--download` to obtain the uploaded CMM configuration file. This feature is supported by the 64MB CMM AST2400 only.
- Use `--skip_precheck` to upload and overwrite the existing system profile.
- `--reboot` and `--post_complete` are required for BMC OOB usage.
- Use the `ProfileManage` command to check the profile list before updating.
- Use the update action `Apply` to immediately update the existing Blade system.
