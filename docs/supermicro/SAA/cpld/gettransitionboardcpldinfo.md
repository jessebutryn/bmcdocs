# GetTransitionboardCpldInfo

Gets the current Transitionboard CPLD information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetTransitionboardCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetTransitionboardCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetTransitionboardCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetTransitionboardCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetTransitionboardCpldInfo
```

## Output

```
Managed system...............................192.168.34.56
 Transitionboard CPLD Version.............00.00.00
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
