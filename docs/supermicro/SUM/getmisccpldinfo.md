# GetMiscCpldInfo

## Description

Use the "GetMiscCpldInfo" command to get the Miscellaneous CPLD firmware image information of NVIDIA MGX™ systems from the managed system.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c GetMiscCpldInfo
```

#### In-Band
```
sum -I Redfish_HI -u <username> -p <password> -c GetMiscCpldInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMiscCpldInfo
Managed system..........................192.168.34.56
 Misc CPLD version...................0B
```

### In-Band Redfish Host Interface
```
[SUM_HOME]# ./sum -c GetMiscCpldInfo -I Redfish_HI -u ADMIN -p ADMIN
The console output contains the following information.
Managed system..........................169.254.3.254
 Misc CPLD version...................0B
```

## Notes

- This command is specific to NVIDIA MGX™ systems.
