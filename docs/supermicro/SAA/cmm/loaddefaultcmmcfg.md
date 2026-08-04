# LoadDefaultCmmCfg

Resets the CMM settings of the managed system to the factory defaults. Allowed option combinations depend on the managed system state; unsupported options are denied.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c LoadDefaultCmmCfg --preserve_user_cfg
saa -i <IP or host name> -u <username> -p <password> -c LoadDefaultCmmCfg --clear_user_cfg --load_unique_password
saa -i <IP or host name> -u <username> -p <password> -c LoadDefaultCmmCfg --clear_user_cfg --load_default_password
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c LoadDefaultCmmCfg --preserve_user_cfg
saa -l <system list file> [-u <username> -p <password>] -c LoadDefaultCmmCfg --clear_user_cfg --load_unique_password
saa -l <system list file> [-u <username> -p <password>] -c LoadDefaultCmmCfg --clear_user_cfg --load_default_password
```

## Options

- `--clear_user_cfg`: Clears user configuration.
- `--preserve_user_cfg`: Preserves user configuration.
- `--load_unique_password`: Loads the CMM unique password.
- `--load_default_password`: Loads the CMM default password.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultCmmCfg --preserve_user_cfg
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultCmmCfg --clear_user_cfg --load_unique_password
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultCmmCfg --clear_user_cfg --load_default_password
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LoadDefaultCmmCfg --preserve_user_cfg
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LoadDefaultCmmCfg --clear_user_cfg --load_unique_password
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LoadDefaultCmmCfg --clear_user_cfg --load_default_password
```

## Notes

- Without the `--user_id` option, the user ID is set to 2 (Administrator) by default.
- `--load_unique_password` only supports systems installed with a CMM unique password.
- This command does not reset any network settings.
- Option combinations and their effect on Reset Network Info, Reset FRU, Reset Users, and ADMIN Password vary — see the SAA User's Guide section 5.7.6 for the full combination table.
