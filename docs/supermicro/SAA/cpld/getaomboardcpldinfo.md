# GetAomboardCpldInfo

Gets the AOM board CPLD firmware image information of the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetAomboardCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetAomboardCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetAomboardCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetAomboardCpldInfo
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c GetAomboardCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetAomboardCpldInfo
```

## Output

```
Managed system.........................192.168.34.56
 AOM Board CPLD version.............CPLD_ID: 270000D0 Rev: 02
```

```
Managed system.........................169.254.3.254
 AOM Board CPLD version..............CPLD_ID: 270000D0 Rev: 02
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
