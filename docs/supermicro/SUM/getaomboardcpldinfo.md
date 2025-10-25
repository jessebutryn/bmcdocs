# GetAomboardCpldInfo

## Description

Use the "GetAomboardCpldInfo" command to get the AOM board CPLD firmware image information of NVIDIA MGX™ systems from the managed system.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c GetAomboardCpldInfo
```

#### In-Band
```
sum -I Redfish_HI -u <username> -p <password> -c GetAomboardCpldInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetAomboardCpldInfo
Managed system..........................192.168.34.56
 AOM Board CPLD version..............CPLD_ID: 270000D0 Rev: 02
```

### In-Band Redfish Host Interface
```
[SUM_HOME]# ./sum -c GetAomboardCpldInfo -I Redfish_HI -u ADMIN -p ADMIN
The console output contains the following information.
Managed system..........................169.254.3.254
 AOM Board CPLD version..............CPLD_ID: 270000D0 Rev: 02
```

## Notes

- This command is specific to NVIDIA MGX™ systems.
