# GetLockdownMode

## Description

When the System Lockdown Mode is enabled on a managed system, neither setting configurations nor updating firmware is allowed in this mode. To learn about the managed system status, use the "GetLockdownMode" command.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c GetLockdownMode
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetLockdownMode [--remote_sum <remote sum path>]
```

## Options

- `--remote_sum <remote sum path>`: Specifies the path to the remote SUM executable (for Remote In-Band).

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetLockdownMode
The console output contains the following information.
Managed system................192.168.34.56
 System Lockdown...........No
```

### In-Band
```
[SUM_HOME]# ./sum -c GetLockdownMode
```

### Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetLockdownMode
The console output contains the following information.
Managed system................localhost
```
