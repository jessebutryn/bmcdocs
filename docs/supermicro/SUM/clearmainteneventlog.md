# ClearMaintenEventLog

Clears the maintenance event log on the managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c ClearMaintenEventLog
```

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ClearMaintenEventLog
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ClearMaintenEventLog
```

## Notes

- Clears maintenance event logs immediately
- Supported for both OOB and in-band usage
