# GetPowerStatus

Gets the current power status of the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetPowerStatus
```

### In-Band
```
saa -c GetPowerStatus
saa -I Redfish_HI -u <username> -p <password> -c GetPowerStatus
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetPowerStatus
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPowerStatus
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetPowerStatus
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c GetPowerStatus
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetPowerStatus
```

## Output

### Standard
```
Managed system................localhost
 Power status..............On
 PSU consumption...........N/A
```

### GB200 System (with power consumption history)
```
Managed system................192.168.34.56
 Power status................On
 PSU consumption...........N/A
 Power Consumption
 Last Hour
 Average Usage...158.083333 (W)
 Max Peak........228 (W)
 Max Peak Time...2024-11-07T01:37:16+00:00
 Min Peak........123 (W)
 Min Peak Time...2024-11-07T01:52:16+00:00
 Last Day
 Average Usage...155.666667 (W)
 Max Peak........241 (W)
 Max Peak Time...2024-11-06T08:57:16+00:00
 Min Peak........64 (W)
 Min Peak Time...2024-11-06T07:57:16+00:00
 Last Week
 Average Usage...105.571429 (W)
 Max Peak........241 (W)
 Max Peak Time...2024-11-07T01:57:16+00:00
 Min Peak........0 (W)
 Min Peak Time...2024-11-01T13:57:16+00:00
```

### Via Redfish Host Interface (with GPU/CPU power consumption)
```
Managed system................192.168.34.56
 System
 Power status..........PoweringOn
 Baseboard
 Power status..........Off
 Power Consumption
 Total GPU.............842.609 (W)
 CPU 1.................89.287000 (W)
 CPU 2.................94.559000 (W)
 GPU 1.................204.876000 (W)
 GPU 2.................228.234000 (W)
 GPU 3.................212.608000 (W)
 GPU 4.................196.884000 (W)
```

## Notes

- If the execution Status field for a managed system is SUCCESS, the BIOS and BMC capabilities of the managed system will be shown in the Execution Message section of the created log file.
