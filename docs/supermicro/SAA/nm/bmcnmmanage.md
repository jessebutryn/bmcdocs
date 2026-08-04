# BmcNmManage

Manages the BMC Intel Node Manager through Intel Intelligent Power Node Manager for Supermicro Intel platforms.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BmcNmManage --type <type> --action <action>
```

### In-Band
```
saa -c BmcNmManage --type <type> --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BmcNmManage --type <type> --action <action>
```

## Actions

Supported for `--type BMC10` (BMC Intel Node Manager 1.0):

- **GetDeviceID**: Gets the BMC device ID.
- **GetPower**: Gets power information from the BMC.
- **GetTemp**: Gets temperature information from the BMC.

## Options

- `--type <type>`: Manages Intel Node Manager with a type. Supported: BMC10.
- `--action <action>`: Manages Intel BMC Node Manager with an action (see Actions above).

## Examples

### GetDeviceID
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcNmManage --type BMC10 --action GetDeviceID
[SAA_HOME]# ./saa -c BmcNmManage --type BMC10 --action GetDeviceID
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BmcNmManage --type BMC10 --action GetDeviceID
```

### GetPower
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcNmManage --type BMC10 --action GetPower
```

### GetTemp
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcNmManage --type BMC10 --action GetTemp
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### GetDeviceID
```
Device ID = 20h
Firmware Version = 0.0.2
IPMI Version = 2.0
Manufacturer ID = 7C 2A 00
Board ID = 27 1D
Raw Data = 20 01 00 02 02 BF 7C 2A 00 27 1D 02 02 00 00
```

### GetPower
```
56 watts
```

## Notes

- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
