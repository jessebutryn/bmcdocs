# MonitorCDUStatus

Shows the current CDU (Coolant Distribution Unit) Web UI status remotely, and can set the CDU alert configuration.

## Syntax

### Getting CDU Status (OOB)
```
saa -i <IP or host name> -u <username> -p <password> -c MonitorCDUStatus {--action <GetStatus|1>} [--file <CDUStatus.txt> [--overwrite]]
```

### Getting CDU Status (Multiple Systems OOB)
```
saa -l <system list file> [-u <username> -p <password>] -c MonitorCDUStatus {--action <GetStatus|1>} [--file <CDUStatus.txt> [--overwrite]]
```

### Setting CDU Alert Config (OOB)
```
saa -i <IP or host name> -u <username> -p <password> -c MonitorCDUStatus --action SetCfg|2 [--file <CDU_alert_setting.json>]
```

### Setting CDU Alert Config (Multiple Systems OOB)
```
saa -l <system list file> [-u <username> -p <password>] -c MonitorCDUStatus --action SetCfg|2 [--file <CDU_alert_setting.json>]
```

## Options

- `--action <action>`: Sets CDU action:
    - `1` = GetStatus
    - `2` = SetCfg
- `--file <file name>`: (Optional) For action 1 = GetStatus: prints the status on screen if the file-saving function is not available, otherwise saves the status to the given file. For action 2 = SetCfg: sets the CDU alert option, monitoring the host with the given JSON file listing device and sensor data records to be monitored.
- `--overwrite`: (Optional) Overwrites the output file.

## Examples

### Getting CDU Status (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MonitorCDUStatus --action GetStatus

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MonitorCDUStatus --action GetStatus --file CDUStatus.txt --overwrite
```

### Getting CDU Status (Multiple Systems OOB)
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c MonitorCDUStatus --action GetStatus --file CDUStatus.txt --overwrite
```

### Setting CDU Alert Config (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MonitorCDUStatus --action SetCfg --file CDU_alert_setting.json
```

### Setting CDU Alert Config (Multiple Systems OOB)
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c MonitorCDUStatus --action SetCfg --file CDU_alert_setting.json
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the CDU status of the managed system is shown in the "Execution Message" section in the created log file.

## Output

```
CDU (Coolant Distribution Unit) System Status
[System Status]
CDU Status: OK
Emergency Status: OK
Operation Mode: auto
[Device Status]
 Device Name Status Value Operation Time(h:m)
 -------------- ------- ------- -------------------
 Power Top OK
 Power Bottom OK
 Pump Left OK 6281[RPM] 108:34
 Pump Right OK 6281[RPM] 108:34
 Valve Left OK 100[%]
 Valve Right OK 100[%]
 CDU Status OK
 Sensor Module OK
 Leak Detection OK
 Humidity Sensor OK
 Liquid Level Low
 Leak (External Ch1) N/A
 Leak (External Ch2) N/A
 Liquid Level (External Ch1) N/A
 Liquid Level (External Ch2) N/A
[Sensor Value]
 Sensor Name Status Value
 -------------- ------- -------
 Temperature from Server Warning level 25.52[°C]
 Temperature to Server Valid 42.15[°C]
 Temperature from Facility Valid 23.20[°C]
 Temperature to Facility Valid 23.12[°C]
 Temperature ambient 20.69[°C]
 Pressure Server Warning level 0.230[MPa]
 Pressure Facility Alert level 0.000[Ma]
 Flow Rate Server Alert level 0.00[L/min]
 Flow Rate Facility Alert level 0.00[L/min]
 Humidity 66.20[%RH]
 Dew Point OK 14.16[°C]
 Heat Load -0.00[kW]
```

## Notes

- The sample CDU alert setting file is named `CDU_alertsetting_sample.json` and is bundled in the SAA release package.
- Device names differ between the CDU Web UI and the JSON file: Leak Detection = `leak`, Power Top = `power1`, Power Button = `power2`, Control Unit = `cunit`, Pump Left = `pump1`, Pump Right = `pump2`, Valve Left = `valv1`, Valve Right = `valv2`, Sensor Module = `sensor`, Humidity Sensor = `humidity`, Liquid Level (OK) = `level_upper`, Liquid Level (Low) = `level_lower`, Liquid Leak (External Ch1)/(Ch2) = `leak_ext_ch1`/`leak_ext_ch2`, Liquid Level (External Ch1)/(Ch2) = `level_ext_ch1`/`level_ext_ch2`.
- Sensor value names: Temperature (From Server) = `temp_from_server`, Temperature (To Server) = `temp_to_server`, Temperature (From Facility) = `temp_from_facility`, Temperature (To Facility) = `temp_to_facility`, Pressure (Server) = `press_server`, Pressure (Facility) = `press_facility`, Flow Rate (Server) = `flow_server`, Flow Rate (Facility) = `flow_facility`.
- Each device's items under `trap` can be set to `true` or `false` to decide whether to trap that item; regardless of trap status, the item still affects overall CDU status.
- Maximum/minimum alert and warning thresholds can be set for Temperature, Pressure, and Flow Rate sensors, for example `temp_from_server` allows 0-80°C for both Alert and Warning levels, `press_server`/`press_facility` allow 0-1 MPa, and `flow_server`/`flow_facility` allow 0-150 L/min.
