# GetKcsPriv

## Description

Use the "GetKcsPriv" command to execute SUM to get the current BMC KCS privilege level from the managed system.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c GetKcsPriv
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetKcsPriv
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetKcsPriv
```

### In-Band
```
[SUM_HOME]# ./sum -c GetKcsPriv
```

### Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetKcsPriv
```

The console output contains the following information.

```
Managed system................192.168.34.56
 KCS Privilege Level.......4 (Administrator)
```
