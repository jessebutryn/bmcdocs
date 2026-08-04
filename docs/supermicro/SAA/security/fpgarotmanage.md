# FpgaRotManage

Manages Motherboard FPGA Root of Trust (RoT) functions on NVIDIA MGX systems: retrieving FPGA/golden image information and updating the golden image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c FpgaRotManage --action <action>
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c FpgaRotManage --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c FpgaRotManage --action <action>
```

## Actions

- **GetInfo**: Retrieves information on active FPGA and golden FPGA.
- **UpdateGolden**: Replaces the golden image with active FPGA firmware.

## Options

- `--action <action>`: Sets action to 1 = GetInfo, 2 = UpdateGolden.

## Examples

### GetInfo
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c FpgaRotManage --action GetInfo
```

### UpdateGolden
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c FpgaRotManage --action UpdateGolden
```

### UpdateGolden (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c FpgaRotManage --action UpdateGolden
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c FpgaRotManage --action UpdateGolden
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
 FPGA version...................0.78
 Golden FPGA version............0.78
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

- This command is specific to NVIDIA MGX systems.
- The execution progress for the managed system is continuously updated in the Execution Message section of the created log file.
