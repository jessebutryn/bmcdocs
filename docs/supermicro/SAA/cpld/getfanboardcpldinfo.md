# GetFanboardCpldInfo

Gets the Fanboard CPLD firmware image information of X13/H13 and later RoT platforms from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetFanboardCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetFanboardCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetFanboardCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFanboardCpldInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c GetFanboardCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetFanboardCpldInfo
```

## Output

```
Managed system...............................192.168.34.56
 [Front CPLD]
 Fanboard CPLD 1 version..............01
 [Rear CPLD]
 Fanboard CPLD 1 version..............01
```

### Fanboard Types

| Type | Description |
|------|-------------|
| Front Fanboard | The first Fanboard. |
| Rear Fanboard | The second Fanboard. |
| Fanboard \<num\> | The third or above Fanboards. |

## Notes

- This command is only available on systems with storage backplanes installed.
- The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
