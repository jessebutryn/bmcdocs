# GetDefaultBiosCfg

Gets the default factory BIOS settings from the managed system and saves them in a USER_SETUP.file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetDefaultBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>]
```

### In-Band
```
saa -c GetDefaultBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c GetDefaultBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetDefaultBiosCfg [--file <USER_SETUP.file> [--overwrite]] [--current_password <current password> | --cur_pw_file <current password file path>]
```

## Options

- `--file <file name>`: Saves the BIOS configuration to a file (prints the default factory BIOS configuration on screen if the file-saving function is not available)
- `--current_password <current password>`: Checks the current BIOS Administrator password
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password
- `--overwrite`: Overwrites the output file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetDefaultBiosCfg --file USER_SETUP.txt --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetDefaultBiosCfg --file USER_SETUP.file --overwrite
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetDefaultBiosCfg --file USER_SETUP.file --overwrite --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetDefaultBiosCfg --file USER_SETUP.file
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetDefaultBiosCfg --file USER_SETUP.file
```

## Notes

- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its default settings are saved in its output file, e.g., `USER_SETUP.file.192.168.34.56`. The `--overwrite` option forces overwrite of an existing file.
- To update BIOS settings based on factory settings: get the factory settings with this command, then follow the same edit/apply workflow as `GetCurrentBiosCfg` (edit the file and use `ChangeBiosCfg`).
