# BladeSummary

Gets summary information for all Blade, switch, and power supply modules of a Supermicro Blade system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BladeSummary
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BladeSummary
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladeSummary
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BladeSummary
```

## Output

```
Blade Module (5/28)
------------------------
Blade | Status
----- | ------
A1 | Normal
 Node | BMC IP | Status
 ---- | ------ | ------
 1 | 12.34.56.78 | Normal
A2 | Normal
 Node | BMC IP | Status
 ---- | ------ | ------
 1 | 12.34.56.78 | Normal
A3 | Normal
 Node | BMC IP | Status
 ---- | ------ | ------
 1 | 12.34.56.78 | Normal
A5 | Normal
 Node | BMC IP | Status
 ---- | ------ | ------
 1 | 12.34.56.78 | Normal
A7 | Normal
 Node | BMC IP | Status
 ---- | ------ | ------
 1 | 12.34.56.78 | Normal

Switch Module (3/4)
------------------------
Switch | Status
------ | ------
A1 | On
A2 | On
B1 | On

Power Supply Module (8/8)
------------------------
Power Supply | Status
------------ | ------
A1 | Normal
A2 | Normal
A3 | Normal
A4 | Normal
B1 | Normal
B2 | Normal
B3 | Normal
B4 | Normal
```

## Notes

- Fan information is only displayed if the CMM Middle Plane is 820 series (check via `GetFruInfo`).
- If the execution Status field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
