# GetMiscCpldInfo

Gets the motherboard Miscellaneous CPLD firmware image information of NVIDIA MGX™ systems from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetMiscCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetMiscCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetMiscCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMiscCpldInfo
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c GetMiscCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMiscCpldInfo
```

## Output

```
Managed system.........................192.168.34.56
 Miscellaneous CPLD version.........0B
```

```
Managed system.........................169.254.3.254
 Miscellaneous CPLD version.........0B
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
