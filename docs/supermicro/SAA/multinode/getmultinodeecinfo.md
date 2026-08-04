# GetMultinodeEcInfo

Gets the multi-node EC firmware image information from the managed system, as well as the local multi-node EC firmware image (with the `--file` option).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetMultinodeEcInfo [--file <filename>]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetMultinodeEcInfo [--file <filename> [--file_only]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetMultinodeEcInfo [--file <filename>]
```

## Options

- `--file <file name>`: (Optional) Reads the multi-node EC information from an input multi-node EC image file.
- `--file_only`: (Optional) Works with the `--file` option, and only reads multi-node EC information from the input image file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMultinodeEcInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetMultinodeEcInfo

[SAA_HOME]# ./saa -c GetMultinodeEcInfo --file EC.bin --file_only
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMultinodeEcInfo
```

## Output

```
Managed system............192.168.34.56
 EC ID.................A7
 EC version............1.20
```

```
Managed system............169.254.3.254
 EC ID.................A7
 EC version............1.20
Local EC image file.......EC.bin
 EC ID.................A7
 EC version............1.20
```

## Notes

- If the execution "Status" field for the managed system is SUCCESS, the multi-node EC firmware image information of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
- This command can only be run on a system on node A to update EC FW for multi nodes.
