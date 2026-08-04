# GetMotherboardMcuInfo

Gets the motherboard MCU firmware image information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetMotherboardMcuInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetMotherboardMcuInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetMotherboardMcuInfo
```

## Options

- `-I Redfish_HI` (Optional): Uses Redfish Host Interface to query the firmware information. (Only in-band usage is supported.)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMotherboardMcuInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetMotherboardMcuInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMotherboardMcuInfo
```

## Output

### Single System
```
Managed system............................192.168.34.56
 Motherboard MCU version...............FF.11.07
```

### Multiple Systems OOB
```
Managed system............................169.254.3.254
 Motherboard MCU version...............FF.11.07
```

The execution progress for the managed system will be continuously updated to the "Execution Message" section of the managed system in the created log file.
