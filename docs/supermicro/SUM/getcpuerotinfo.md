# GetCpuERoTInfo

## Description

Use the "GetCpuERoTInfo" command to get the ERoT CPU firmware image information of NVIDIA MGX™ systems from the managed system.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c GetCpuERoTInfo
```

#### In-Band
```
sum -I Redfish_HI -u <username> -p <password> -c GetCpuERoTInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCpuERoTInfo
Managed system..........................192.168.34.56
 [CPU 0]
 ERoT version....................01.03.0103.0000_n01
 [CPU 1]
 ERoT version....................01.03.0103.0000_n01
```

### In-Band Redfish Host Interface
```
[SUM_HOME]# ./sum -c GetCpuERoTInfo -I Redfish_HI -u ADMIN -p ADMIN
The console output contains the following information.
Managed system..........................169.254.3.254
 [CPU 0]
 ERoT version....................01.03.0103.0000_n01
 [CPU 1]
 ERoT version....................01.03.0103.0000_n01
```

## Notes

- This command is specific to NVIDIA MGX™ systems.
