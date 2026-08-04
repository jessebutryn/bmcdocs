# GetCmmUserList

Gets the current CMM user list from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetCmmUserList
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetCmmUserList
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCmmUserList
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetCmmUserList
```

## Output

```
Maximum number of Users : 16
Count of currently enabled Users : 1
User ID | User Name | Privilege Level | Enabled | Account Types
======= | ==================== | =============== | ======= | ===================
 2 | ADMIN | Administrator | Yes | Redfish/IPMI
======= | ==================== | =============== | ======= | ===================
```

## Notes

- If the execution Status field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
