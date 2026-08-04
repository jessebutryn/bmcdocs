# ClearCMOS

Clears CMOS and resets all BIOS settings to their default values.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ClearCMOS --ac_cycle
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c ClearCMOS --ac_cycle
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ClearCMOS --ac_cycle
```

## Options

- `--ac_cycle`: Proceeds to AC cycle the managed system after the operation.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ClearCMOS --ac_cycle
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c ClearCMOS --ac_cycle
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ClearCMOS --ac_cycle
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```
