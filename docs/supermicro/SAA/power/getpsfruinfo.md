# GetPsFruInfo

Gets the current PSFRU (Power Supply Field Replaceable Unit) information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetPsFruInfo
```

### In-Band
```
saa -c GetPsFruInfo
```

### Multiple Systems OOB
```
saa -l <system list file> -u <username> -p <password> -c GetPsFruInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPsFruInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetPsFruInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetPsFruInfo
```

## Output

```
[Module 1](SlaveAddress = 0x70)
 Status: On
 Temperature: 60
 Fan 1: 6688 RPM
 Fan 2: N/A
```

## Notes

- If the execution Status field of the managed system shows SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
