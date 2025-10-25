# GetMotherboardFpgaInfo

## Description

Use the "GetMotherboardFpgaInfo" command to get the motherboard FPGA firmware image information of NVIDIA MGX™ systems from the managed system.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c GetMotherboardFpgaInfo
```

#### In-Band
```
sum -I Redfish_HI -u <username> -p <password> -c GetMotherboardFpgaInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMotherboardFpgaInfo
Managed system............................192.168.34.56
 Motherboard FPGA version..............0.78
```

### In-Band Redfish Host Interface
```
[SUM_HOME]# ./sum -c GetMotherboardFpgaInfo -I Redfish_HI -u ADMIN -p ADMIN
The console output contains the following information.
Managed system............................169.254.3.254
 Motherboard FPGA version..............0.78
```

## Notes

- This command is specific to NVIDIA MGX™ systems.
