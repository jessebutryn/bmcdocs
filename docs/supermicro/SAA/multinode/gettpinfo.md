# GetTpInfo

Gets the current TwinPro settings from the managed system and saves them to a configuration file (e.g. TpInfo.xml).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetTpInfo [--file <filename> [--overwrite]]
```

### In-Band
```
saa -c GetTpInfo [--file <filename> [--overwrite]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetTpInfo [--file <filename> [--overwrite]]
```

## Options

- `--file <file name>`: (Optional) Saves the configuration to a file. Prints the TwinPro configuration on the screen if the file-saving function is not available.
- `--overwrite`: (Optional) Overwrites the output file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetTpInfo --file TpInfo.xml --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetTpInfo --file TpInfo.xml --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetTpInfo --file TpInfo.xml --overwrite
```

## Notes

- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its current settings are stored in its output file, e.g., `TpInfo.xml.192.168.34.56`.
- The `--overwrite` option is used to force overwrite the existing file, e.g., `TpInfo.xml.192.168.34.56`.
