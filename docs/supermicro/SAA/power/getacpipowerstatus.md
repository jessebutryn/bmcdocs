# GetAcpiPowerStatus

Gets the current ACPI (Advanced Configuration and Power Interface) status of the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetAcpiPowerStatus
```

### In-Band
```
saa -c GetAcpiPowerStatus
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetAcpiPowerStatus
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetAcpiPowerStatus
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetAcpiPowerStatus
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetAcpiPowerStatus
```

## Output

```
ACPI Power Status: S0/G0 Working
```

## Notes

- If the execution Status field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
