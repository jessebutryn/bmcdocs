# GetPsuInfo

## Description

Use the "GetPsuInfo" command to get the current PSU information from the managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetPsuInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPsuInfo
```

### In-Band
```
[SUM_HOME]# ./sum -c GetPsuInfo
```

The console output contains the following information.

```
[Module 1](SlaveAddress = 0x78)
 PWS Module Number: PWS-605P-1H
 PWS Serial Number: P605A0E39B07611
 PWS Revision: REV1.1
 PMBus Revision: 0x8B22
 Status: [STATUS OK](00h)
 AC Input Voltage: 122.00 V
 AC Input Current: 0.46 A
 DC 12V Output Voltage: 12.38 V
 DC 12V Output Current: 4.50 A
 Temperature 1: 25 C
 Temperature 2: 53 C
 Fan 1: 2688 RPM
 Fan 2: N/A
 DC 12V Output Power: 55 W
 AC Input Power: 55 W
```
