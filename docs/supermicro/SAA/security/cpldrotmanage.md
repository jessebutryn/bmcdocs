# CpldRotManage

Manages CPLD Root of Trust (RoT) functions on RoT systems of X13 RoT2.0 and later platforms: retrieving CPLD/golden image information and updating the golden CPLD image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CpldRotManage --action <action>
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c CpldRotManage --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CpldRotManage --action <action>
```

## Actions

- **GetInfo**: Retrieves information on active CPLD and golden CPLD.
- **UpdateGolden**: Replaces the golden image with active CPLD firmware.

## Options

- `--action <action>`: Sets action to 1 = GetInfo, 2 = UpdateGolden.

## Examples

### GetInfo (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CpldRotManage --action GetInfo
```

### UpdateGolden (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CpldRotManage --action UpdateGolden
```

### UpdateGolden (In-Band through Redfish Host Interface)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c CpldRotManage --action UpdateGolden
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CpldRotManage --action UpdateGolden
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### GetInfo
```
Managed system.....................192.168.34.56
 CPLD version...................F5.07.02
 Golden CPLD version............F5.07.01
```

### UpdateGolden
```
Status: System is backing up current FW as golden image. Please wait for 2
minutes.
........................................
........................................
Done
Status: Please check golden FW version for result.
```

## Notes

- This command is supported on RoT systems of X13 RoT2.0 and later platforms.
