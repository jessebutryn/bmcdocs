# GetMaintenEventLog

Shows the managed system's current maintenance event logs (including both BIOS and BMC maintenance event logs). Both `--st` and `--et` options are used to show logs at a specified time range. With `--count`, shows the specified number of logs. With `--file`, the maintenance event log can be saved in a MaintenEventLog.txt file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetMaintenEventLog [--st <start time> --et <end time>] [--count <log count>] [--file <MaintenEventLog.txt> [--overwrite]]
```

### In-Band
```
saa -c GetMaintenEventLog [--st <start time> --et <end time>] [--count <log count>] [--file <MaintenEventLog.txt> [--overwrite]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetMaintenEventLog [--st <start time> --et <end time>] [--count <log count>] [--file <MaintenEventLog.txt> [--overwrite]]
```

## Options

- `--st <start time>`: Enters the start time in YYYYMMDD format
- `--et <end time>`: Enters the end time in YYYYMMDD format
- `--file <file name>`: Saves the maintenance event log to a file (prints on screen if the file-saving function is not available)
- `--count <maintenance log count>`: Enters the log count (if zero, the entire maintenance event log is displayed)
- `--overwrite`: Overwrites the output file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMaintenEventLog --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMaintenEventLog --count 5 --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMaintenEventLog --st 20200601 --et 20200602 --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMaintenEventLog --st 20200601 --et 20200602 --count 5 --file MaintenEventLog.txt --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetMaintenEventLog --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -c GetMaintenEventLog --count 5 --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -c GetMaintenEventLog --st 20200601 --et 20200602 --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -c GetMaintenEventLog --st 20200601 --et 20200602 --count 5 --file MaintenEventLog.txt --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMaintenEventLog --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMaintenEventLog --count 5 --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMaintenEventLog --st 20200601 --et 20200602 --file MaintenEventLog.txt --overwrite
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMaintenEventLog --st 20200601 --et 20200602 --count 5 --file MaintenEventLog.txt --overwrite
```

## Notes

- If the "Status" field of a managed system (e.g., 192.168.34.56) shows SUCCESS, its maintenance event logs are stored in its output file, e.g., `MaintenEventLog.txt.192.168.34.56`. The `--overwrite` option forces overwrite of an existing file.
- If the `--file` option is not used, the event logs of each managed system will be shown in its "Execution Message" section in the created execution log file.
