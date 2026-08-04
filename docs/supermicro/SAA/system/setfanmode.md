# SetFanMode

Sets the fan mode for the target system. Afterwards, use `GetFanMode` to confirm the desired mode was set successfully.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetFanMode --fanmode <fan type>
```

### In-Band
```
saa -c SetFanMode --fanmode <fan type>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetFanMode --fanmode <fan type>
```

## Options

- `--fanmode <Fan Mode Type>`: Sets the fan mode:
    - `0` = Standard
    - `1` = Full
    - `2` = Optimal
    - `3` = PUE2 Optimal
    - `4` = Heavy IO
    - `5` = PUE3 Optimal
    - `6` = Liquid Cooling
    - `7` = Smart
    - `8` = PUE Optimal
    - `9` = Smart Cooling
    - `10` = Performance
    - `11` = Silent

  The input type string is converted to the above type number.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetFanMode --fanmode 0
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetFanMode --fanmode 0
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

```
Fan mode is changed to Standard
All Available Fan Modes are:
Mode: Type
0: Standard
1: Full
2: Optimal
4: Heavy IO
```
