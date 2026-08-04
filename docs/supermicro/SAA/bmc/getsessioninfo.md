# GetSessionInfo

Gets BMC RMCP session information.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSessionInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSessionInfo
```

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSessionInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSessionInfo
```

## Output

```
Managed system............................192.168.34.56
 SessionHandler........................01h
 Number of possible active sessions....60
 Number of currently active sessions...1
 User ID...............................02h
 Operating Privilege Level.............04h
 Session protocol auxiliary data.......11h
 IP Address of remote console..........C0 A8 00 64 (192.168.0.100)
 Mac Address of remote console.........00 00 00 00 00 00 (00:00:00:00:00:00)
 Port Number...........................85 94 (38021)
```
