# ChangeVROCCfg

Updates the VROC configuration on the managed system using an edited VROC.cfg.xml file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeVROCCfg --file <filename>
```

### In-Band
```
saa -c ChangeVROCCfg --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeVROCCfg --file <filename>
```

## Options

- `--file <file name>`: Updates the VROC with the given configuration file.
- `--individually`: Updates each VROC key with the corresponding configuration file individually (optional). Required for multiple systems usage.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeVROCCfg --file VROC.cfg.xml
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeVROCCfg --file VROC.cfg.xml
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeVROCCfg --file VROC.cfg.xml --individually
```

## Notes

- Use `--individually` to update each managed system with the corresponding configuration file concurrently; this option is required for multiple-systems usage of this command.
- If the execution Status field for a managed system is SUCCESS, its VROC settings are updated.
- To update multiple systems (e.g., 192.168.34.56 and 192.168.34.57), provide two files named VROC.cfg.xml.192.168.34.56 and VROC.cfg.xml.192.168.34.57, and set `--file` to `VROC.cfg.xml`. With `--individually`, SAA searches for the per-system files to update each system respectively.
