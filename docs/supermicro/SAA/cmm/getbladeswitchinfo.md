# GetBladeSwitchInfo

Gets the switch firmware image information from the managed system, as well as information from a local switch firmware image file (with the `--file` option).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBladeSwitchInfo [--dev_id <Device ID>] [--file <filename>]
```

### In-Band
```
saa -c GetBladeSwitchInfo --file <filename> --file_only
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBladeSwitchInfo [--dev_id <Device ID>] [--file <filename>]
```

## Options

- `--file <file name>`: Reads the switch information from an input switch image file.
- `--dev_id <Device ID>`: Assigns switch index. Switch index: `[A1,A2,B1,B2]` or `[ALL]`.
- `--file_only`: Works with `--file`, and only reads switch image information from the input image file.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c GetBladeSwitchInfo --file Supermicro_Switch.bin --file_only
```

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBladeSwitchInfo
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBladeSwitchInfo --dev_id A1,A2
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBladeSwitchInfo --file Supermicro_Switch.bin
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBladeSwitchInfo --dev_id A1,A2 --file Supermicro_Switch.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBladeSwitchInfo
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBladeSwitchInfo --dev_id A1,A2 --file Supermicro_Switch.bin
```

## Output

```
Local switch image file..Supermicro_Switch.bin
 Module name..........BMB-25G-P10
 Switch version.......1.0.0.21
Managed system...........192.168.34.56
[Switch A1]
==============
Switch IP............192.168.34.100
Switch type..........25G Pass-thru Module
Module name..........SBM-25G-P10 (P1)
Switch version.......1.0.0.21
Power Status.........On
Status...............Normal
[Switch A2]
==============
Switch IP............192.168.34.101
Switch type..........25G Pass-thru Module
Module name..........SBM-25G-P10 (P1)
Switch version.......1.0.0.8
Power Status.........On
Status...............Normal
[Switch B1]
==============
Switch IP............192.168.34.102
Switch type..........25G Pass-thru Module
Module name..........SBM-25G-P10 (P1)
Switch version.......1.0.0.21
Power Status.........On
Status...............Normal
[Switch B2]
==============
Switch IP............192.168.34.103
Switch type..........25G Pass-thru Module
Module name..........SBM-25G-P10 (P1)
Switch version.......1.0.0.21
Power Status.........On
Status...............Normal
```

## Notes

- SBM-25G-P10 and BMB-25G-P10 are the same switch module.
- The `--file` option is used to parse SBM-25G-P10/BMB-25G-P10/MBM-XEM-002/MBM-GEM-004/SBM-25G-100 firmware images.
- The execution progress for the managed system will be continuously updated to the Execution Message section of the created log file.
