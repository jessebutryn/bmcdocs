# ChangeRaidCfg

Updates RAID configuration on the managed system using a RAID configuration file.

## Prerequisites

1. Get current RAID configuration (see GetRaidCfg)
2. Edit configurable values in the RAID configuration file
3. Optionally set Action attribute to "None" for unchanged tables
4. Optionally remove unchanged tables/elements

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c ChangeRaidCfg --file <RAIDCfg.xml>
```

## Options

- `--file <RAIDCfg.xml>`: Required. RAID configuration file

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeRaidCfg --file RAIDCfg.xml
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ChangeRaidCfg --file RAIDCfg.xml
```

## Notes

- Requires SFT-DCMS-SINGLE license
- Configuration changes are applied immediately
- Only supported for OOB usage
