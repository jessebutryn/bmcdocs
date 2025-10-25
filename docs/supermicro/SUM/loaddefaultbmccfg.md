# LoadDefaultBmcCfg

Resets the BMC configuration of the managed system to factory defaults.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c LoadDefaultBmcCfg [--preserve_user_cfg] [--clear_user_cfg [--load_unique_password | --load_default_password]]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c LoadDefaultBmcCfg [--preserve_user_cfg] [--clear_user_cfg [--load_unique_password | --load_default_password]] [--remote_sum <remote sum path>]
```

## Options

- `--preserve_user_cfg`: Preserves user configuration (network, users info, FRU, ADMIN password).
- `--clear_user_cfg`: Clears user configuration.
- `--load_unique_password`: Loads unique pre-programmed password (only for systems with BMC unique password).
- `--load_default_password`: Loads default "ADMIN" password.
- `--reboot`: Forces the managed system to reboot (in-band only).

## Reset Behavior

| Option | Network Reset | Users Info Reset | FRU Reset | ADMIN Password |
|--------|---------------|------------------|-----------|----------------|
| `--preserve_user_cfg` | No | No | No | Preserved |
| `--clear_user_cfg --load_default_password` | No | Yes | No | ADMIN |
| `--clear_user_cfg --load_unique_password` | No | Yes | No | Unique Password |

## Examples

### OOB Preserve User Config
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --preserve_user_cfg
```

### OOB Clear User Config with Unique Password
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --clear_user_cfg --load_unique_password
```

### OOB Clear User Config with Default Password
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --clear_user_cfg --load_default_password
```

### In-Band Preserve User Config
```
[SUM_HOME]# ./sum -c LoadDefaultBmcCfg --preserve_user_cfg [--reboot]
```

### In-Band Clear User Config with Unique Password
```
[SUM_HOME]# ./sum -c LoadDefaultBmcCfg --clear_user_cfg --load_unique_password [--reboot]
```

### In-Band Clear User Config with Default Password
```
[SUM_HOME]# ./sum -c LoadDefaultBmcCfg --clear_user_cfg --load_default_password [--reboot]
```

### Remote In-Band Preserve User Config
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c LoadDefaultBmcCfg --preserve_user_cfg [--reboot]
```

## Notes

- The --load_unique_password option only supports systems installed with a BMC unique password.
- This command will not reset any network settings.
- Allowed option combinations depend on the managed system state. Unsupported option combinations will be denied.
- All new X10, X11, X12, H11, H12, and future generation Supermicro products ship with a "Unique Pre-Programmed Password" instead of the default "ADMIN" password.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/loaddefaultbmccfg.md