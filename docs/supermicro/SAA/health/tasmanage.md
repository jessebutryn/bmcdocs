# TasManage

Executes TAS (thin agent) related actions on the managed system. TAS must be installed on the managed system before using this command.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c TasManage --action <action> [--period <update period>]
```

### In-Band
```
saa -c TasManage --action <action> [--period <update period>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c TasManage --action <action> [--period <update period>]
```

## Options

- `--action <action>`: Sets TAS action:
    - `GetInfo`: Retrieves information from TAS.
    - `Pause`: Pauses the TAS service.
    - `Resume`: Resumes the TAS service.
    - `Refresh`: Triggers TAS to recollect data.
    - `Clear`: Clears the collected TAS data in the BMC.
    - `SetPeriod`: Sets the TAS update period.
- `--period <seconds>`: (Optional) Sets the TAS update period in seconds (between 5 and 60).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TasManage --action GetInfo

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TasManage --action Pause

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TasManage --action Resume

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TasManage --action Refresh

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TasManage --action Clear
```

### In-Band
```bash
[SAA_HOME]# ./saa -c TasManage --action SetPeriod --period 5

[SAA_HOME]# ./saa -c TasManage --action GetInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c TasManage --action GetInfo

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c TasManage --action Pause

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c TasManage --action Resume
```

If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system is shown in the "Execution Message" section of the created log file.

## Output

### GetInfo
```
Item | Value
---- | -----
Version | 1.7.0
Build Data | 220503
Protocol Version | 0x01
Status | Stopped
TAS Start Time | Fri Aug 11 22:36:05 2023
Last Update Time | Fri Aug 11 22:45:50 2023
```
