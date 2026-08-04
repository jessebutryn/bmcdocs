# CpuERotManage

Manages CPU ERoT (External Root of Trust) functions on NVIDIA MGX systems: retrieving CPU ERoT/golden image information, updating the golden image, and recovering the CPU ERoT.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CpuERotManage --action <action>
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c CpuERotManage --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CpuERotManage --action <action>
```

## Actions

- **GetInfo**: Retrieves information about the active ERoT CPU and the golden ERoT CPU.
- **UpdateGolden**: Replaces the golden image with active ERoT CPU firmware.
- **Recover**: Recovers ERoT CPU from the backup image or the golden image. By priority, the managed system recovers ERoT CPU from the backup image; if the backup image is corrupted, it then recovers from the golden image.

## Options

- `--action <action>`: Sets action to 1 = GetInfo, 2 = UpdateGolden, 3 = Recover.

## Examples

### GetInfo
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CpuERotManage --action GetInfo
```

### UpdateGolden
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CpuERotManage --action UpdateGolden
```

### Recover
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CpuERotManage --action Recover
```

### UpdateGolden (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c CpuERotManage --action UpdateGolden
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CpuERotManage --action UpdateGolden
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
 CPU ERoT 0 version.............01.03.0103.0000_n01
 Golden CPU ERoT version........01.03.0103.0000_n01
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

### Recover
```
Status: System is recovering ERoT CPU firmware image. Please wait for 2 minutes.
........................................
........................................
Done
Status: Please check golden FW version for result.
```

## Notes

- This command is specific to NVIDIA MGX systems.
- The execution progress for the managed system is continuously updated in the Execution Message section of the created log file.
