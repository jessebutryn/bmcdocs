# GetDefaultBiosCfg

## Description

Use the "GetDefaultBiosCfg" command to execute SUM to get the default factory BIOS settings from the managed system and save it in the USER_SETUP.file file.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c GetDefaultBiosCfg --file <USER_SETUP.file> [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--overwrite]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetDefaultBiosCfg --file <USER_SETUP.file> [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--overwrite] [--remote_sum <remote sum path>]
```

## Options

- `--file <USER_SETUP.file>`: Specifies the file to save the BIOS settings.
- `--current_password <current password>`: Specifies the current BIOS password.
- `--cur_pw_file <current password file path>`: Specifies the file containing the current BIOS password.
- `--overwrite`: Overwrites the output file if it exists.
- `--remote_sum <remote sum path>`: Specifies the path to the remote SUM executable (for Remote In-Band).

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetDefaultBiosCfg --file USER_SETUP.txt --overwrite
```

### In-Band
```
[SUM_HOME]# ./sum -c GetDefaultBiosCfg --file USER_SETUP.file --overwrite
```

### Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetDefaultBiosCfg --file USER_SETUP.file --overwrite --remote_sum /root/sum
```
