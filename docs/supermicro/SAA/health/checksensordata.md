# CheckSensorData

Checks the sensor data for the managed system, including showing sensor readings and thresholds, deleting an SDR entry, and getting or setting the SDR version.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CheckSensorData [--action <action> [--sdr_id <id>] [--sdr_major_version <version> --sdr_minor_version <version>]] [--redfish] [--temp_unit <unit>] [--showall]
```

### In-Band
```
saa -c CheckSensorData [-I Redfish_HI -u <username> -p <password>] [--action <action> [--sdr_id <id>] [--sdr_major_version <version> --sdr_minor_version <version>]] [--showall]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CheckSensorData [--action <action> [--sdr_id <id>] [--sdr_major_version <version> --sdr_minor_version <version>]] [--redfish] [--temp_unit <unit>] [--showall]
```

## Options

- `--action <action>`: (Optional) Sets action:
    - `1` = Show
    - `2` = Del
    - `3` = GetVer
    - `4` = SetVer
- `--redfish`: (Optional) Enables support for pure Redfish.
- `--sdr_id <id>`: (Optional) The SDR ID for delete.
- `--sdr_major_version <version>`: (Optional) The SDR major version.
- `--sdr_minor_version <version>`: (Optional) The SDR minor version.
- `--temp_unit <unit>`: (Optional) The unit of the temperature to display, either C or F.
- `--showall`: (Optional) Shows all IPMI sensor threshold values of the managed system.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSensorData

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSensorData --action Show --showall

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSensorData --action Del --sdr_id 4

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSensorData --action GetVer

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSensorData --action SetVer --sdr_major_version 0 --sdr_minor_version 255

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSensorData --temp_unit F

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSensorData --redfish --action Show
```

### In-Band
```bash
[SAA_HOME]# ./saa -c CheckSensorData --action Show

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c CheckSensorData --action Show
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CheckSensorData
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the sensor data of the managed system is shown in the "Execution Message" section in the created log file.

## Output

### CPU Temperature Sensor (default)
```
Status | (#)Sensor | Reading | Low Limit | High Limit |
------ | --------- | ------- | --------- | ---------- |
OK | (4) CPU Temp | 41C/106F | 5C/41F | 104C/219F |
```

### CPU Temperature Sensor (--showall)
```
Status | (#)Sensor | Reading | Low NR | Low CT | Low NC | High NC | High CT | High NR |
------ | --------- | ------- | ------ | ------ | ------- | ------- | ------- | ------- |
OK | (4) CPU Temp | 42C/108F | 5C/41F | 5C/41F | 10C/50F | 99C/210F | 104C/219F | 104C/219F |
```

### CPU Temperature Sensor (--temp_unit F)
```
Status | (#)Sensor | Reading | Low NR | Low CT | Low NC | High NC | High CT | High NR |
------ | --------- | ------- | ------ | ------ | ------- | ------- | ------- | ------- |
OK | (4) CPU Temp | 108F | 41F | 41F | 50F | 210F | 219F | 219F |
```

### BMC Sensor
```
Status | (#)Sensor | Reading | Lower Caution | Lower Critical | Lower Fatal | Upper Caution | Upper Critical | Upper Fatal |
------ | --------- | ------- | --------------- | -------------- | ----------- | --------------- | -------------- | ----------- |
OK | (#)BMC 1.0V | 1.014V | 0.000V | 0.887V | 0.000V | 0.000V | 1.092V | 0.000V |
```

### VBAT Sensor (Redfish Host Interface)
```
Status | (#)Sensor | Reading | Low Limit | High Limit |
------ | --------- | ------- | --------- | ---------- |
OK | (#)VBAT | Battery Presence Detected |
```

## Notes

- Supported sensors vary between different motherboards and firmware images.
- Network add-on card temperature can be retrieved from some X10 or later systems.
- For PS and Chassis Intrusion sensors, the "Reading" field is used only for debugging; you only need to check that the "Status" field shows "OK."
- The Redfish protocol supports only the `--action Show` option.
