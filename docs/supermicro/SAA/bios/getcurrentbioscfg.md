# GetCurrentBiosCfg

Gets the current BIOS settings from the managed system and saves them in a USER_SETUP.file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetCurrentBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>] [--filter <filter type>] [--tui [--compact]]
```

### In-Band
```
saa -c GetCurrentBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>] [--filter <filter type>] [--tui [--compact]]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c GetCurrentBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>] [--filter <filter type>] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetCurrentBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>] [--filter <filter type>]
```

## Options

- `--file <file name>`: Saves the BIOS configuration to a file (prints on screen if file-saving is unavailable)
- `--current_password <current password>`: Checks the current BIOS Administrator password
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password
- `--overwrite`: Overwrites the output file
- `--filter <filter type>`: Sets filter type to `1` = nondefault
- `--tui`: Edits the BIOS configuration with a text-based user interface (not supported for Remote In-Band usage)
- `--compact`: Generates a compact version of the BIOS configuration containing only the settings changed in the TUI

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCurrentBiosCfg --file USER_SETUP.file --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetCurrentBiosCfg --file USER_SETUP.file --filter nondefault
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetCurrentBiosCfg --file USER_SETUP.file --overwrite --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetCurrentBiosCfg --file USER_SETUP.file
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetCurrentBiosCfg --file USER_SETUP.file
```

## Notes

- This BIOS configuration file is synchronized to the BMC from the BIOS when the system reboots or powers up.
- If the BMC firmware image has been reflashed, this function will not work until the managed system is first rebooted or powered up.
- The current BIOS settings are generated as an XML file containing extended ASCII characters; use ISO 8859-1 encoding to view the file.
- Use `--filter nondefault` to generate a configuration file that includes only settings where the current value differs from the default.
- Use `--tui` to view the BIOS configuration in a text-based user interface.
- Use `--compact` to generate a compact version of the configuration file in TUI by removing unchanged BIOS settings.
- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its current settings are stored in its output file, e.g., `USER_SETUP.file.192.168.34.56`. The `--overwrite` option forces overwrite of an existing file.
