# GetRaidCfg

## Description

Use the "GetRaidCfg" command to execute SUM to get the current RAID settings from the managed system and save it in the RAIDCfg.xml file.

## Notes

- The received tables/elements between the two managed systems might not be identical. Only the supported tables/elements for the managed system will be received.
- The SUM cannot get or change the RAID configurations of JBOD mode setting under the Controller Properties in an in-band environment.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetRaidCfg --file <RAIDCfg.xml> [--overwrite]
```

## Options

- `--file <RAIDCfg.xml>`: Specifies the file to save the RAID configuration.
- `--overwrite`: Overwrites the output file if it exists.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetRaidCfg --file RAIDCfg.xml --overwrite
```

### In-Band
```
[SUM_HOME]# ./sum -c GetRaidCfg --file RAIDCfg.xml --overwrite
```
