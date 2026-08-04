# ChangeRaidCfg

Updates the RAID configuration on the managed system using an edited RAIDCfg.xml file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeRaidCfg --file <filename>
```

### In-Band
```
saa -c ChangeRaidCfg --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeRaidCfg --file <filename>
```

## Options

- `--file <file name>`: Updates the RAID with the given configuration file.
- `--individually`: Updates each managed system with the corresponding configuration file individually (optional).
- `--controller <Controller>`: Vendor of the RAID controller — `Broadcom` or `Marvell` (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeRaidCfg --file RAIDCfg.xml
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeRaidCfg --file RAIDCfg.xml
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeRaidCfg --file RAIDCfg.xml
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeRaidCfg --file RAIDCfg.xml --individually
```

## Notes

- Some table settings cannot be uniformly applied to each managed system. You might need to change the table's action to `None`, or remove those tables/elements from the configuration file, when preparing the file to update multiple systems.
- Use `--individually` to update each managed system with the corresponding configuration file concurrently.
- SAA cannot get or change the RAID configurations of the JBOD mode setting under Controller Properties in an in-band environment.
- If the execution Status field for a managed system is SUCCESS, its RAID settings are updated.
- To update multiple systems (e.g., 192.168.34.56 and 192.168.34.57), provide two files named RAIDCfg.xml.192.168.34.56 and RAIDCfg.xml.192.168.34.57, and set `--file` to `RAIDCfg.xml`. With `--individually`, SAA searches for the per-system files to update each system respectively.
