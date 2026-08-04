# LoadDefaultBmcCfg

Resets the BMC of the managed system to factory default settings. Allowed option combinations depend on the managed system state; unsupported combinations are denied.

Supermicro systems no longer use the default password "ADMIN" for new devices — all such systems ship with a "Unique Pre-Programmed Password" for the admin user. See the BMC Unique Password Guide for details on locating it.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c LoadDefaultBmcCfg {--preserve_user_cfg | --clear_user_cfg {--load_default_password | --load_unique_password [--load_default_lan [--load_default_fru]]}} [--bmc_boot_check [--reboot [--post_complete]]] [--redfish]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c LoadDefaultBmcCfg {--preserve_user_cfg | --clear_user_cfg {--load_default_password | --load_unique_password [--load_default_lan [--load_default_fru]]}} [--bmc_boot_check [--reboot]] [--redfish]
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c LoadDefaultBmcCfg {--preserve_user_cfg | --clear_user_cfg {--load_default_password | --load_unique_password [--load_default_lan [--load_default_fru]]}} [--bmc_boot_check [--reboot]] [--redfish] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c LoadDefaultBmcCfg {--preserve_user_cfg | --clear_user_cfg {--load_default_password | --load_unique_password [--load_default_lan [--load_default_fru]]}} [--bmc_boot_check [--reboot [--post_complete]]] [--redfish]
```

## Options

- `--reboot`: Forces the managed system to reboot or power up after operation
- `--redfish`: Enables support for pure Redfish
- `--clear_user_cfg`: Clears user configuration
- `--preserve_user_cfg`: Preserves user configuration (network config, users, and FRU are all preserved)
- `--load_unique_password`: Loads the unique BMC password (only works on systems installed with a unique BMC password)
- `--load_default_password`: Loads the default BMC password
- `--load_default_lan`: Loads the default BMC LAN configuration
- `--load_default_fru`: Loads the default FRU configuration
- `--bmc_boot_check`: Checks if BMC is booted up after reset
- `--post_complete`: Waits for the managed system's POST to complete after rebooting

## Action/Reset Behavior

| Option combination | Reset Network Cfg | Reset User | Reset FRU | Password set to |
|---|---|---|---|---|
| `--preserve_user_cfg` | N | N | N | Preserved |
| `--clear_user_cfg` with `--load_default_password` | N | Y | N | ADMIN |
| `--clear_user_cfg` with `--load_unique_password` | N | Y | N | Unique Password |
| `--clear_user_cfg` with `--load_unique_password` and `--load_default_lan` | Y | Y | N | Unique Password |
| `--clear_user_cfg` with `--load_unique_password`, `--load_default_lan`, and `--load_default_fru` | Y | Y | Y | Unique Password |

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c LoadDefaultBmcCfg --preserve_user_cfg --bmc_boot_check --reboot --post_complete
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --clear_user_cfg --load_unique_password
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --clear_user_cfg --load_default_password
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --clear_user_cfg --load_unique_password --load_default_lan --load_default_fru
```

### In-Band
```bash
[SAA_HOME]# ./saa -c LoadDefaultBmcCfg --preserve_user_cfg
[SAA_HOME]# ./saa -c LoadDefaultBmcCfg --clear_user_cfg --load_unique_password
[SAA_HOME]# ./saa -c LoadDefaultBmcCfg --clear_user_cfg --load_default_password
[SAA_HOME]# ./saa -c LoadDefaultBmcCfg --clear_user_cfg --load_unique_password --load_default_lan --load_default_fru
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c LoadDefaultBmcCfg --preserve_user_cfg
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --preserve_user_cfg
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --clear_user_cfg --load_unique_password
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LoadDefaultBmcCfg --clear_user_cfg --load_default_password
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c LoadDefaultBmcCfg --clear_user_cfg --load_default_password
```

## Notes

- The `--load_unique_password` option only works on systems installed with a unique BMC password.
- The `--bmc_boot_check` option is not compatible with in-band pure Redfish usage on X14/B14 systems, because resetting the BMC configuration disables the Redfish host interface by default on these systems.
- The `--bmc_boot_check` option is not supported for in-band Redfish command mode.
