# ChangeBmcLANCfg

Updates BMC LAN settings on the managed system using a configuration file.

## Prerequisites

1. Get current BMC LAN settings (see GetBmcLANCfg)
2. Edit configurable values in the BMC LAN configuration file
3. Optionally set Action attribute to "None" for unchanged tables
4. Optionally remove unchanged tables/elements

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c ChangeBmcLANCfg --file <BMCLANCfg.xml>
```

## Options

- `--file <BMCLANCfg.xml>`: Required. BMC LAN configuration file

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBmcLANCfg --file BMCLANCfg.xml
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ChangeBmcLANCfg --file BMCLANCfg.xml
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c ChangeBmcLANCfg --file BMCLANCfg.xml --overwrite
```

## Notes

- Connection may break if LAN configuration is changed
- For in-band: All `<Configurations>` elements in `<LAN>` are configurable
- For OOB without Redfish: All `<LAN>` configurations are read-only
- For OOB: `<DynamicIPv6>` and `<StaticIPv6>` elements are read-only
