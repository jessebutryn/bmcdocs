# BladePsuManage

Manages the Blade power supply unit (PSU) for Supermicro Blade systems, including PSU information, power consumption, and fan speed/mode.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BladePsuManage --action <action> [--value <value>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BladePsuManage --action <action> [--value <value>]
```

## Actions

- **GetBladePsuInfo**: Displays Blade PSU information.
- **GetBladePsuConsumption**: Displays power consumption of the Blade system power supply module.
- **GetFanSpeed**: Gets Blade system fan speed.
- **SetFanSpeed**: Sets Blade system fan speed.
- **GetFanMode**: Gets Blade system fan mode.
- **SetFanMode**: Sets Blade system fan mode.

## Options

- `--action <action>`: Sets the action to perform (see Actions above).
- `--value <value>`: Assigns a value (optional; used with `SetFanSpeed` and `SetFanMode`).
  - For `SetFanSpeed`: fan speed level `[1-10]`.
  - For `SetFanMode`: `0` = Auto, `1` = Manual.

## Examples

### GetBladePsuInfo
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladePsuManage --action GetBladePsuInfo
```

### GetBladePsuConsumption
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladePsuManage --action GetBladePsuConsumption
```

### GetFanSpeed
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladePsuManage --action GetFanSpeed
```

### SetFanSpeed
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladePsuManage --action SetFanSpeed --value 5
```

### GetFanMode
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladePsuManage --action GetFanMode
```

### SetFanMode
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladePsuManage --action SetFanMode --value 0
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BladePsuManage --action GetBladePsuInfo
```

## Output

### GetBladePsuInfo
```
PSU A1
==========
Item | Value
---- | -----
Power Supply | Power Supply A1
Model Name | PWS-DF006-2F
Power Status | On
Temperature (°C) | 45
Fan1 Speed (RPM) | 10877
Fan2 Speed (RPM) | 11793
AC Input Voltage | N/A
Max Watt | N/A
AC Input Current | N/A
DC Output Current | N/A
Current Power Usage | N/A
FW Version | 1.0
FRU Version | 1
Error | Normal

PSU A2
==========
Item | Value
---- | -----
Power Supply | Power Supply A2
Model Name | PWS-2K21A-BR
Power Status | On
Temperature (°C) | 44
Fan1 Speed (RPM) | 12137
Fan2 Speed (RPM) | 11106
AC Input Voltage | 117 V
Max Watt | 1200 W
AC Input Current | 3.19 A
DC Output Current | 20 A
Current Power Usage | 20.00 %
FW Version | 1.0
FRU Version | 1
Error | Normal

Fan C1
==========
Fan | Fan C1
Model Name | N/A
Power Status | N/A
Fan1 Speed (RPM) | N/A
Fan2 Speed (RPM) | N/A
Fan3 Speed (RPM) | N/A
```

### GetBladePsuConsumption
```
| Module | Power Consumption (W) |
| ------ | --------------------- |
| PS A1 | 195 |
| PS A2 | 208 |
| PS A3 | 207 |
| PS A4 | 209 |
| PS B1 | 222 |
| PS B2 | 222 |
| PS B3 | 194 |
| PS B4 | 221 |
| | |
| Total | 1678 |
```

### GetFanSpeed
```
Current Fan Speed Level: 5
```

### GetFanMode
```
Current Fan Mode: Manual
```

## Notes

- If the execution Status field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
