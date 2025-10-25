# GetBmcUserList

Use the "GetBmcUserList" command to get the current BMC user list from the managed system.

## Syntax

```
sum -i <IP or host name> -u <username> -p <password>] -c GetBmcUserList
```

## Examples

### OOB

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcUserList
```

### In-band

```
[SUM_HOME]# ./sum -c GetBmcUserList
```

## Notes

- "Account Types" is not supported on platforms before X12/H12.
- "Account Types" is only supported for OOB usage.