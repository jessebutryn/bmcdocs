# GetAipCpldInfo

Gets the current AIP (AI Processor) CPLD information from the managed system installed with AIP. This command is OOB only.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetAipCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetAipCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetAipCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetAipCpldInfo
```

## Output

```
AIP CPLD information
====================
Managed system..........................192.168.34.56
 [AIP Device 1]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
 [AIP Device 2]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
 [AIP Device 3]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
 [AIP Device 4]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
 [AIP Device 5]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
 [AIP Device 6]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
 [AIP Device 7]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
 [AIP Device 8]
 AIP Model.......................Habana Gaudi HL205
 AIP CPLD version................1A
```

## Notes

- This command is supported on the SYS-420GH-TNGR system.
- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
- This command is OOB only.
