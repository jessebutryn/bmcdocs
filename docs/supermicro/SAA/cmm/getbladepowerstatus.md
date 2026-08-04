# GetBladePowerStatus

Gets the current power status of the Blade system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBladePowerStatus
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBladePowerStatus
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBladePowerStatus
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBladePowerStatus
```

## Output

```
Blade | Node | Power
------------|---------|----------
Blade A1 | Node 1 | On
Blade A2 | Node 1 | On
Blade A3 | Node 1 | On
Blade A4 | Node 1 | On
Blade A5 | Node 1 | On
Blade A6 | Node 1 | On
Blade A7 | Node 1 | On
Blade A8 | Node 1 | On
Blade A9 | Node 1 | On
Blade A10 | Node 1 | On
```

## Notes

- If the Status field for a managed system shows SUCCESS, the power status of the Blade system will be shown in the Execution Message section of the created log file.
