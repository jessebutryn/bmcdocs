# GetGpuERoTInfo

## Description

Use the "GetGpuERoTInfo" command to get the External RoT (ERoT) GPU firmware image information of NVIDIA MGX™ systems from the managed system.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c GetGpuERoTInfo
```

#### In-Band
```
sum -I Redfish_HI -u <username> -p <password> -c GetGpuERoTInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetGpuERoTInfo
Managed system..........................192.168.34.56
 [GPU 0]
 ERoT version....................01.03.0103.0000_n01
```

### In-Band Redfish Host Interface
```
[SUM_HOME]# ./sum -c GetGpuERoTInfo -I Redfish_HI -u ADMIN -p ADMIN
The console output contains the following information.
Managed system..........................169.254.3.254
 [GPU 0]
 ERoT version....................01.03.0103.0000_n01
```

## Notes

- This command is specific to NVIDIA MGX™ systems.
