# ChangeCmmCfg

Updates the CMM configuration on the managed system using a CmmCfg.xml file, or uploads/updates the CMM configuration via a CMM profile.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeCmmCfg --file <CmmCfg.xml> [--skip_unknown] [--precheck]
saa -i <IP or host name> -u <username> -p <password> -c ChangeCmmCfg {--upload --file <CmmCfg.xml> [--skip_precheck] | --update Apply | Deploy [--skip_unknown] [--precheck]}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeCmmCfg --file <CMMCfg.xml> [--skip_unknown] [--precheck] [--individually]
saa -l <system list file> [-u <username> -p <password>] -c ChangeCmmCfg {--upload --file <CmmCfg.xml> [--skip_precheck] | --update Apply | Deploy [--skip_unknown] [--precheck]}
```

## Options

- `--file <file name>`: Updates the CMM with the given configuration file.
- `--upload`: Uploads the CMM configuration file to CMM for updating profiles (optional).
- `--update <update rule>`: Updates the CMM configurations with the existing profile on CMM. Supported update rule: `Apply` (optional).
- `--individually`: Updates each CMM with the corresponding configuration file individually (optional).
- `--precheck`: Checks the configurations before update (optional).
- `--skip_unknown`: Skips the unknown tables or settings in the CMM configuration file (optional).
- `--skip_precheck`: Uploads and overwrites the existing CMM profile (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeCmmCfg --file CmmCfg.xml
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeCmmCfg --upload --file CmmCfg.xml
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeCmmCfg --update Apply
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeCmmCfg --file CMMCfg.xml
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeCmmCfg --file CMMCfg.xml --individually
```

## Notes

- If the Status field of a managed system shows SUCCESS, its CMM settings are updated.
- To update multiple systems (e.g., 192.168.34.56 and 192.168.34.57), provide two files named CMMCfg.xml.192.168.34.56 and CMMCfg.xml.192.168.34.57, and set `--file` to `CMMCfg.xml`. With `--individually`, SAA searches for the per-system files to update each system respectively.
- The connection might be lost if the LAN configuration is changed.
- Use the `GetCmmCfg` command with `--download` to obtain the CMM configuration file for use with `--upload` (64MB CMM AST2400 only).
- Use `--skip_precheck` to upload and overwrite the existing CMM profile.
- The update action `Apply` updates the CMM immediately with a CMM profile. If the scheduled update time in the CMM profile has expired, the CMM configuration is updated immediately; otherwise it is updated at the scheduled time.
- For multiple systems usage, some table settings (e.g., LAN configurations) cannot be applied uniformly to each managed system — you may need to set the table's action to `None` or remove the table/element from the configuration file.
- `--skip_unknown` skips all invalid tables and settings in the latest CMM configuration on the managed system.
