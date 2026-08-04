# GetBackplaneCpldInfo

Gets the backplane CPLD firmware information from the backplane on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBackplaneCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetBackplaneCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBackplaneCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBackplaneCpldInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetBackplaneCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBackplaneCpldInfo
```

## Output

```
Backplane CPLD information
==========================
Managed system..........................192.168.34.56
 [Backplane 0]
 Backplane CPLD ID...............0023
 Backplane CPLD Revision.........0C
```

## Notes

- The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
