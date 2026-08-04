# GetScpInfo

Gets the System Control Processor (SCP) firmware image information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetScpInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetScpInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetScpInfo
```

## Options

- `--file_only`: Works with the `--file` option, and only reads SCP information from the input image file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetScpInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetScpInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetScpInfo
```

## Output

```
Managed system......................192.168.34.56
 SCP version.....................2.0a
```

## Notes

- If the execution "Status" field of a managed system is SUCCESS, the SCP information of the managed system will be shown in its "Execution Message" section in the created log file.
