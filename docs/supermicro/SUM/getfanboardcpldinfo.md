# GetFanboardCpldInfo

## Description

Use the "GetFanboardCpldInfo" command to get the Fanboard CPLD firmware image information of X13/H13 and later RoT platforms from the managed system.

## Syntax

```
sum [-i <IP or host name> | -I Redfish_HI] -u <username> -p <password> -c GetFanboardCpldInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFanboardCpldInfo
Managed system...............................192.168.34.56
 [Front CPLD]
 Fanboard CPLD 1 version..............01
 [Rear CPLD]
 Fanboard CPLD 1 version..............01
```

### In-Band Redfish Host Interface
```
[SUM_HOME]# ./sum -c GetFanboardCpldInfo -I Redfish_HI -u ADMIN -p ADMIN
The console output contains the following information.
Managed system...............................192.168.34.56
 [Front CPLD]
 Fanboard CPLD 1 version..............01
 [Rear CPLD]
 Fanboard CPLD 1 version..............01
```

## Notes

- This command is specific to X13/H13 and later RoT platforms.
