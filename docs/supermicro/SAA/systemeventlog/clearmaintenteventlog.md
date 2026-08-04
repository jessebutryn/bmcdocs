# ClearMaintenEventLog

Clears the maintenance event log for the target system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ClearMaintenEventLog [--gen_log]
```

### In-Band
```
saa -c ClearMaintenEventLog [--gen_log]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ClearMaintenEventLog [--gen_log]
```

## Options

- `--gen_log`: Generates a log entry indicating the successful clearing of the maintenance event log

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ClearMaintenEventLog
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ClearMaintenEventLog --gen_log
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ClearMaintenEventLog
[SAA_HOME]# ./saa -c ClearMaintenEventLog --gen_log
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ClearMaintenEventLog
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ClearMaintenEventLog --gen_log
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
