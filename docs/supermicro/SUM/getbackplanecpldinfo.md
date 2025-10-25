# GetBackplaneCpldInfo

## Description

Use the "GetBackplaneCpldInfo" command to get the backplane CPLD firmware information from the backplane on managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetBackplaneCpldInfo
```

## Options

None.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBackplaneCpldInfo
The console output contains the following information.
Backplane CPLD information
==========================
Managed system..........................192.168.34.56
 [Backplane 0]
 Backplane Model.................BPN-NVMe4-217BHQ-S6
 Backplane CPLD ID...............0023
 Backplane CPLD Revision.........0C
```

### In-Band
```
[SUM_HOME]# ./sum -c GetBackplaneCpldInfo
The console output contains the following information.
Backplane CPLD information
==========================
Managed system..........................localhost
 [Backplane 0]
 Backplane Model.................BPN-NVMe4-217BHQ-S6
 Backplane CPLD ID...............0023
 Backplane CPLD Revision.........0C
```

## Notes

- This command is only available on X10/H10 and later platforms with storage backplanes installed.
- A maximum of four backplane CPLDs can be detected.
