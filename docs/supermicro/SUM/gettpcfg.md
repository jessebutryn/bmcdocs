# GetTpCfg

## Description

Use the "GetTpCfg" command to execute SUM to get the current TwinPro settings from the managed system and save it in the TpCfg.xml file.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetTpCfg --file <TpCfg.xml> [--overwrite]
```

## Options

- `--file <TpCfg.xml>`: Specifies the file to save the TwinPro configuration.
- `--overwrite`: Overwrites the output file if it exists.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetTpCfg --file TpCfg.xml --overwrite
```

### In-Band
```
[SUM_HOME]# ./sum -c GetTpCfg --file TpCfg.xml --overwrite
```
