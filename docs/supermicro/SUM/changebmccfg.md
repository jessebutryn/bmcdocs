# ChangeBmcCfg

Updates the BMC configuration on the managed system using a configuration file.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c ChangeBmcCfg --file <BMCCfg.xml|BMCCfg.bin> [--restore]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c ChangeBmcCfg --file <BMCCfg.xml|BMCCfg.bin> [--restore]
```

## Options

- `--file <BMCCfg.xml|BMCCfg.bin>`: BMC configuration file to apply (XML or binary format)
- `--restore`: Restores BMC configuration with the corresponding read-only configuration file

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBmcCfg --file BMCCfg.xml
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBmcCfg --file BMCCfg.bin --restore
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ChangeBmcCfg --file BMCCfg.xml
[SUM_HOME]# ./sum -c ChangeBmcCfg --file BMCCfg.bin --restore
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c ChangeBmcCfg --file BMCCfg.xml
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c ChangeBmcCfg --file BMCCfg.bin --restore
```

## Prerequisites

1. Get current BMC settings (see GetBmcCfg)
2. Edit configurable values in the BMC configuration file
3. Optionally set Action attribute to "None" for unchanged tables
4. Optionally remove unchanged tables/elements

## Notes

- Connection may break if LAN configuration is changed
- For in-band: All `<Configurations>` elements in `<LAN>` are configurable
- For OOB without Redfish: All `<LAN>` configurations are read-only
- For OOB: `<DynamicIPv6>` and `<StaticIPv6>` are read-only
- For OOB with account lockout support: `<Account>` table replaces `<UserManagement>`
- Since SUM 2.12.0: Supports pure Redfish LAN table
