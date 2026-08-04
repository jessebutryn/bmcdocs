# NmMeManage

Manages the Intel Management Engine (ME) through Intel Intelligent Power Node Manager for Supermicro Intel platforms.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c NmMeManage --type <type> --action <action>
```

### In-Band
```
saa -c NmMeManage --type <type> --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c NmMeManage --type <type> --action <action>
```

## Actions

Supported for `--type NM20` (Node Manager 2.0):

- **GetDeviceID**: Gets the ME device ID.
- **Reset**: Reboots ME.
- **ResetToDefault**: Resets ME to default.
- **EnterToUpdateMode**: Forces ME to update mode.
- **PowerOff**: Sets ME power state off.
- **SelfTest**: Gets self-test results.
- **Mode**: Gets ME running mode.
- **ListImagesInfo**: Lists ME images information.
- **GetPower**: Gets power information from ME.
- **GetTemp**: Gets temperature information from ME.

## Options

- `--type <type>`: Manages Intel Node Manager with type. Supported: NM20.
- `--action <action>`: Manages Intel Node Manager with the action to perform (see Actions above).

## Examples

### GetDeviceID
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action GetDeviceID
[SAA_HOME]# ./saa -c NmMeManage --type NM20 --action GetDeviceID
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action GetDeviceID
```

### Reset
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action Reset
```

### ResetToDefault
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action ResetToDefault
```

### EnterToUpdateMode
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action EnterToUpdateMode
```

### PowerOff
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action PowerOff
```

### SelfTest
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action SelfTest
```

### Mode
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action Mode
```

### ListImagesInfo
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action ListImagesInfo
```

### GetPower
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action GetPower
```

### GetTemp
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmMeManage --type NM20 --action GetTemp
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### Mode
```
ME is in NORMAL mode.
```

### ListImagesInfo
```
Recovery Image:
Image Type = recovery image
raw = 57 01 00 02 01 02 07 35 00
1st operational Image:
Image Type = operational image 1 (This Image is currently running)
raw = 57 01 00 02 01 02 07 35 05
2nd operational Image:
Image Type = operational image 2
raw = 57 01 00 02 01 02 07 35 02
```

### GetPower
```
56 watts
```

### GetTemp
```
56 (C)
```

## Notes

- Starting from X14 and later platforms, the `NmMeManage` command is not supported since these platforms do not have a Management Engine (ME) to support Intel Node Manager management.
- If the BMC status is S0/S1, ME cannot be powered off immediately; a "not support in present state" message is displayed. To power off ME, turn off the chassis power first.
- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
