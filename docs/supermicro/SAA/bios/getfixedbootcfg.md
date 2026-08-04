# GetFixedBootCfg

Gets the fixed boot order configuration of the managed system. Only supports X13 platforms or later.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetFixedBootCfg [--file <filename>] [--overwrite] --redfish
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetFixedBootCfg [--file <filename>] [--overwrite] --redfish
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetFixedBootCfg --file <USER_SETUP.file> [--overwrite] --redfish
```

## Options

- `--file <file name>`: Saves the configuration to a file (prints the BIOS fixed boot order configuration on screen if the file-saving function is not available)
- `--redfish`: Gets the BIOS fixed boot order with the pure Redfish solution
- `--overwrite`: Overwrites the output file

## Examples

### OOB
```bash
./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFixedBootCfg --redfish --file FixedBootCfg.xml --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c GetFixedBootCfg --redfish --file FixedBootCfg.xml --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l Slist.txt -u ADMIN -p PASSWORD -c GetFixedBootCfg --file USER_SETUP.file --overwrite --redfish
```

## Notes

- The Get Fixed Boot Configuration command only supports X13 platforms or later.
