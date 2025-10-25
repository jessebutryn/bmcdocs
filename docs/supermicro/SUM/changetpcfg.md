# ChangeTpCfg

Updates TwinPro configuration on the managed system using a TwinPro configuration file.

## Prerequisites

1. Get current TwinPro settings (see GetTpCfg)
2. Edit configurable values in the TwinPro configuration file
3. Optionally set Action attribute to "None" for unchanged tables
4. Optionally remove unchanged tables/elements

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c ChangeTpCfg --file <TpCfg.xml>
```

## Options

- `--file <TpCfg.xml>`: Required. TwinPro configuration file

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeTpCfg --file TpCfg.xml
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ChangeTpCfg --file TpCfg.xml
```

## Notes

- Configuration changes are applied immediately
- Supported for both OOB and in-band usage
