# NmCpuManage

Manages CPU configuration by Intel Intelligent Power Node Manager for Supermicro Intel platforms.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c NmCpuManage --type <type> --action <action> [options...]
```

### In-Band
```
saa -c NmCpuManage --type <type> --action <action> [options...]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c NmCpuManage --type <type> --action <action> [options...]
```

## Actions

Supported for `--type NM20` (Node Manager 2.0):

- **GetPState**: Gets the maximum allowed CPU P-State.
- **GetTState**: Gets the maximum allowed CPU T-State.
- **GetPTState**: Gets the CPU P-State and T-State.
- **GetCPUCores**: Gets the maximum allowed logical processors.
- **GetCPUMemTemp**: Gets the CPU/Memory temperature.
- **GetHostCPUData**: Gets the host CPU data.
- **SetMaxAllowedPState**: Sets the maximum allowed CPU P-State.
- **SetMaxAllowedTState**: Sets the maximum allowed CPU T-State.
- **SetMaxAllowedCPUCores**: Sets the maximum allowed logical processors.

Supported for `--type NM40` (Node Manager 4.0):

- **GetTurboSyncRatio**: Gets the turbo synchronization ratio.
- **SetTurboSyncRatio**: Sets the turbo synchronization ratio.

## Options

- `--type <type>`: Manages CPU with type. Supported: NM20, NM40.
- `--action <action>`: Manages CPU with the action to perform (see Actions above).
- `--value <Assignment value>`: Assigns value. Used with SetMaxAllowedPState (check number of P-States via GetPState), SetMaxAllowedTState (check number of T-States via GetTState), and SetMaxAllowedCPUCores (check number of logical cores via GetCPUCores).
- `--socket <Socket number>`: Assigns CPU socket number (used with GetTurboSyncRatio/SetTurboSyncRatio). 0-7 for which current settings should be read; 255 = all sockets return common maximum settings.
- `--limit <limit>`: Assigns limit (used with SetTurboSyncRatio, the Turbo Ratio Limit). 0 = restore default settings; other values = the Turbo Ratio Limit to set.
- `--core <Core number>`: Assigns core number (used with GetTurboSyncRatio, active cores configuration). 255 = all sockets return common maximum settings.

## Examples

### GetPState / GetTState / GetPTState
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action GetPState
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action GetTState
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action GetPTState
```

### GetCPUCores / GetCPUMemTemp / GetHostCPUData
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action GetCPUCores
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action GetCPUMemTemp
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action GetHostCPUData
```

### SetMaxAllowedPState / SetMaxAllowedTState / SetMaxAllowedCPUCores
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action SetMaxAllowedPState --value 0
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action SetMaxAllowedTState --value 0
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action SetMaxAllowedCPUCores --value 0
```

### GetTurboSyncRatio
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM40 --action GetTurboSyncRatio --socket 0 --core 255
```

### SetTurboSyncRatio
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCpuManage --type NM40 --action SetTurboSyncRatio --socket 0 --limit 0
```

### In-Band
```bash
[SAA_HOME]# ./saa -c NmCpuManage --type NM20 --action GetPState
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c NmCpuManage --type NM20 --action GetPState
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### GetPState
```
Current maximum allowed P-State: 0
Number of P-State: 16
```

### GetTState
```
Current maximum allowed T-State: 0
Number of T-State: 1
```

### GetPTState
```
P-State: High |#_______________| Low [0/16] (Current/Number of State)
T-State: High |#| Low [0/1] (Current/Number of State)
```

### GetCPUCores
```
Current maximum allowed cores: 152
Number of logical cores on the platform: 152
Number of installed processor packages: 2
Number of logical cores on each processor: 76
```

### GetCPUMemTemp
```
CPU#0 = 38(c) (TJMax = 104, DTS = 66)
CPU#1 = 35(c) (TJMax = 104, DTS = 69)
[CPU#0]CHANNEL#0, DIMM#0 = 39(c)
[CPU#0]CHANNEL#2, DIMM#0 = 38(c)
[CPU#1]CHANNEL#0, DIMM#0 = 39(c)
[CPU#1]CHANNEL#2, DIMM#0 = 37(c)
```

### GetHostCPUData
```
Host CPU data:
End of POST notification was received
Host CPU discovery data is valid
Number of P-States = 16
Number of T-States = 1
Number of installed CPUs/socket = 2
Processor Discovery Data-1 = 00 00 00 00 00 00 00 00
Processor Discovery Data-2 = 00 00 00 00 00 00 00 00
```

### SetMaxAllowedPState / SetMaxAllowedTState / SetMaxAllowedCPUCores
```
NmCpuManage command is completed.
```

### SetTurboSyncRatio
```
Done
```

## Notes

- Starting from X14 and later platforms, the `--type NM20` and `NM40` options are not supported. These platforms do not have a Management Engine (ME) to support Intel Node Manager management.
- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
