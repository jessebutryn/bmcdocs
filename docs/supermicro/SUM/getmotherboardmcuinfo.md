# GetMotherboardMcuInfo

## Description

Use the "GetMotherboardMcuInfo" command to get the motherboard MCU firmware image information from the managed system.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c GetMotherboardMcuInfo
```

#### In-Band
```
sum -I Redfish_HI -u <username> -p <password> -c GetMotherboardMcuInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMotherboardMcuInfo
Managed system............................192.168.34.56
 Motherboard MCU version...............FF.11.07
```

### In-Band Redfish Host Interface
```
[SUM_HOME]# ./sum -c GetMotherboardMcuInfo -I Redfish_HI -u ADMIN -p ADMIN
The console output contains the following information.
Managed system............................169.254.3.254
 Motherboard MCU version...............FF.11.07
```
