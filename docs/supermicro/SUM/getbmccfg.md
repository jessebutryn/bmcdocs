# GetBmcCfg

Gets the current BMC settings from the managed system and saves them to a file.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c GetBmcCfg --file <BMCCfg.xml|BMCCfg.bin> [--dump] [--overwrite]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetBmcCfg --file <BMCCfg.xml|BMCCfg.bin> [--dump] [--overwrite]
```

## Options

- `--file <BMCCfg.xml|BMCCfg.bin>`: Output file for BMC configuration (XML or binary format)
- `--dump`: Dumps read-only BMC configuration file (saves as .bin)
- `--overwrite`: Overwrites the output file if it exists

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcCfg --file BMCCfg.xml --overwrite
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcCfg --file BMCCfg.bin --dump --overwrite
```

### In-Band
```bash
[SUM_HOME]# ./sum -c GetBmcCfg --file BMCCfg.xml --overwrite
[SUM_HOME]# ./sum -c GetBmcCfg --file BMCCfg.bin --dump --overwrite
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetBmcCfg --file BMCCfg.xml --overwrite
```

## Notes

- Received tables/elements may not be identical between systems; only supported ones are received
- File formats may differ between in-band and OOB usage
- Syslog table is accessed via HTTPS; information lost if HTTPS disabled
- For OOB, if BMC supports account lockout, `<Account>` table replaces `<UserManagement>`
- Since SUM 2.12.0, supports pure Redfish LAN table in BMC configuration
