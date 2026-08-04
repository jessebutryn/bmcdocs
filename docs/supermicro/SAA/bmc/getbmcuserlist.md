# GetBmcUserList

Gets the current BMC user list from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBmcUserList
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetBmcUserList
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c GetBmcUserList [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBmcUserList
```

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcUserList
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetBmcUserList
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetBmcUserList
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetBmcUserList --remote_saa /root/saa
```

### Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p ADMIN --oi 192.168.34.56 --ou root --op 111111 -c GetBmcUserList --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBmcUserList
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetBmcUserList
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c GetBmcUserList
```

## Output

```
Maximum number of Users : 16
Count of currently enabled Users : 1
User ID | User Name | Privilege Level | Enabled | Account Types
======= | ==================== | =============== | ======= | ===================
 2 | ADMIN | Administrator | Yes | Redfish/IPMI
======= | ==================== | =============== | ======= | ===================
The BMC user list.
```

### Multiple Systems OOB (mixed BMC capabilities)
```
Maximum number of Users : 10
Count of currently enabled Users : 1
User ID | User Name | Privilege Level | Enabled
======= | ==================== | =============== | =======
 2 | ADMIN | Administrator | Yes
======= | ==================== | =============== | =======
The BMC user list.
Maximum number of Users : 16
Count of currently enabled Users : 1
User ID | User Name | Privilege Level | Enabled | Account Types
======= | ==================== | =============== | ======= | ===================
 2 | ADMIN | Administrator | Yes | Redfish/IPMI
======= | ==================== | =============== | ======= | ===================
The BMC user list.
```

## Notes

- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
