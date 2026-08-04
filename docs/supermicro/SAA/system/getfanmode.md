# GetFanMode

Retrieves the fan configuration of the managed system, including the current fan mode and all available fan modes supported by the system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetFanMode
```

### In-Band
```
saa -c GetFanMode
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetFanMode
```

## Options

None

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFanMode
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetFanMode
```

## Output

```
Current FanMode is "Optimal".
All Available Fan Mode are:
Mode: Type
0: Standard
1: Full
2: Optimal
4: Heavy IO
```

## Notes

Supported fan modes are:

| Mode | Type |
|------|------|
| 0 | Standard |
| 1 | Full |
| 2 | Optimal |
| 3 | PUE2 Optimal |
| 4 | Heavy IO |
| 5 | PUE3 Optimal |
| 6 | Liquid Cooling |
| 7 | Smart |
| 8 | PUE Optimal |
| 9 | Smart Cooling |
| 10 | Performance |
| 11 | Silent |

The set of modes actually available depends on the managed system, as shown in the "All Available Fan Mode" output.
