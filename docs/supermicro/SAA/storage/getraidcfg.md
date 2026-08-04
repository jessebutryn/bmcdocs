# GetRaidCfg

Gets the current RAID settings from the managed system and saves them to a RAIDCfg.xml file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetRaidCfg --file <filename> [--overwrite]
```

### In-Band
```
saa -c GetRaidCfg --file <filename> [--overwrite]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetRaidCfg --file <filename> [--overwrite]
```

## Options

- `--file <file name>`: Saves the configuration to a file. Prints the RAID configuration on screen if the file-saving function is not available (optional).
- `--overwrite`: Overwrites the output file (optional).
- `--controller <Controller>`: Vendor of the RAID controller — `Broadcom` or `Marvell` (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetRaidCfg --file RAIDCfg.xml
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetRaidCfg --file RAIDCfg.xml --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetRaidCfg --file RAIDCfg.xml --overwrite
```

## Notes

- The received tables/elements between two managed systems might not be identical. Only the supported tables/elements for the managed system will be received.
- SAA cannot get or change the RAID configurations of the JBOD mode setting under Controller Properties in an in-band environment.
- If the execution Status field for a managed system (e.g., 192.168.34.56) is SUCCESS, its current settings are stored in its output file, e.g., RAIDCfg.xml.192.168.34.56. The `--overwrite` option forces the overwrite of an existing file of that name.
