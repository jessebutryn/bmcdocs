# GetMaintenEventLog

## Description

Use the "GetMaintenEventLog" command to have SUM show the managed system's current maintenance event logs (including both BIOS and BMC maintenance event logs). Both --st and --et options are used to show logs at the specified time. With the "--count" option, the GetMaintenEventLog command can show the specified number of logs. With the "--file" option, the maintenance event log can be saved in a MaintenEventLog.txt file.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetMaintenEventLog [--st <start time> --et <end time>] [--count <log count>] [--file <MaintenEventLog.txt> [--overwrite]]
```

## Options

- `--st <start time>`: Specifies the start time for the logs (format: YYYYMMDD).
- `--et <end time>`: Specifies the end time for the logs (format: YYYYMMDD).
- `--count <log count>`: Specifies the number of logs to show.
- `--file <MaintenEventLog.txt>`: Saves the maintenance event log to the specified file.
- `--overwrite`: Overwrites the output file if it exists.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMaintenEventLog --st 20200601 --et 20200602 --count 5 --file MaintenEventLog.txt --overwrite
```

### In-Band
```
[SUM_HOME]# ./sum -c GetMaintenEventLog --file MaintenEventLog.txt --overwrite
```
