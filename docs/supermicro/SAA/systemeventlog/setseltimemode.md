# SetSELTimeMode

Sets the SEL (System Event Log) time of the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetSELTimeMode --time <time>
```

### In-Band
```
saa -c SetSELTimeMode --time <time>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetSELTimeMode --time <time>
```

## Options

- `--time <Time>`: Sets the SEL time format, either `YYYYMMDDhhmmss` or `YYYYMMDDhhmm`

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetSELTimeMode --time 20240716120000
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SetSELTimeMode --time 202407161200
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetSELTimeMode --time 20240716120000
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
