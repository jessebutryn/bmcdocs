# GetLockdownMode

Gets the BMC System Lockdown Mode status from the managed system. When System Lockdown Mode is enabled, neither setting configurations nor updating firmware is allowed.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetLockdownMode
```

### In-Band
```
saa -c GetLockdownMode
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetLockdownMode
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetLockdownMode
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetLockdownMode
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetLockdownMode
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

```
Managed system................192.168.34.56
 System Lockdown...........No
Managed system................localhost
 System Lockdown...........No
```
