# GetPowerStatus

## Description

Use the "GetPowerStatus" command to get the current power status of the managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetPowerStatus
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPowerStatus
The console output contains the following information.
Managed system................192.168.34.56
 Power status..............On
```

### In-Band
```
[SUM_HOME]# ./sum -c GetPowerStatus
The console output contains the following information.
Managed system................localhost
 Power status..............On
```
