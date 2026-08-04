# GetCmmCfg

Gets the current CMM settings from the managed system and saves them to a CmmCfg.xml file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetCmmCfg [--file <CmmCfg.xml>] [--overwrite] [--download [--profile_repo]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetCmmCfg --file <CmmCfg.xml> [--overwrite] [--download [--profile_repo]]
```

## Options

- `--file <file name>`: Saves the configuration to a file. Prints the CMM configuration on screen if the file-saving function is not available (optional).
- `--download`: Downloads the current CMM configuration file that supports profile update from CMM (optional).
- `--profile_repo`: Downloads the existing CMM profile from CMM (optional).
- `--overwrite`: Overwrites the output file (optional).
- `--action <action>`: Sets the action for each XML table. Acceptable options: `None` or `Change` (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCmmCfg --file CmmCfg.xml --overwrite
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCmmCfg --download --file CmmCfg.xml --overwrite
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCmmCfg --download --profile_repo --file CmmCfg_Cache.xml --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetCmmCfg --file CmmCfg.xml --overwrite
```

## Notes

- Received tables/elements might not be identical between two managed systems. Only tables/elements supported for the managed system will be received.
- Configuration files in XML can be downloaded from CMM through the `--download` option. This feature is supported by 64MB CMM AST2400 only.
- If the Status field of a managed system (e.g., 192.168.34.56) shows SUCCESS, its current settings are stored in its output file, e.g., CMMCfg.xml.192.168.34.56. The `--overwrite` option forces the overwrite of an existing file of that name.
