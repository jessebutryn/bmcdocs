# GetSwitchInfo

## Description

Use the "GetSwitchInfo" command to get the switch firmware image information as well as the local switch firmware image (with the --file option) from the managed system.

## Notes

- SBM-25G-P10 and BMB-25G-P10 are the same switch module.
- The --file option is used to parse SBM-25G-P10/BMB-25G-P10/MBM-XEM-002/MBM-GEM-004/SBM-25G-100 firmware image.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetSwitchInfo [--dev_id <Device ID>] [--file <filename> [--file_only]]
```

## Options

- `--dev_id <Device ID>`: Specifies the device ID(s) of the switch(es), e.g., A1,A2.
- `--file <filename>`: Specifies the switch firmware image file to read information from.
- `--file_only`: Reads information only from the local file specified by --file.

## Examples

### In-Band
```
[SUM_HOME]# ./sum -c GetSwitchInfo --file Supermicro_Switch.bin --file_only
```

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSwitchInfo
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSwitchInfo --dev_id A1,A2
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSwitchInfo --file Supermicro_Switch.bin
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSwitchInfo --dev_id A1,A2 --file Supermicro_Switch.bin
```

The console output contains the following information.

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
```
