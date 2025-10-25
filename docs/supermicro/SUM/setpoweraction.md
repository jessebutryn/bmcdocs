# SetPowerAction

Sets the type of power action for the managed system.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c SetPowerAction --action <action> --blade [<Blade_Index> | ALL] [--node <Node Index>]
```

### OpenBMC
```
sum -l <system list file> [-u <username> -p <password>] -c SetPowerAction --action <action>
```

## Options

- `--action <action>`: Sets the power action to perform.
  - `up`: Power up the managed system.
  - `0`: Power down the managed system.
- `--blade [<Blade_Index> | ALL]`: Specifies the blade index (for blade systems).
- `--node <Node Index>`: Specifies the node index (optional).

## Examples

### OOB Power Up
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetPowerAction --action up
```

### OOB Power Down
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetPowerAction --action 0
```

### In-Band Power Up
```
[SUM_HOME]# ./sum -c SetPowerAction --action up
```

### In-Band Power Down
```
[SUM_HOME]# ./sum -c SetPowerAction --action 0
```

### OpenBMC Power Up
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c SetPowerAction --action up
```

### OpenBMC Power Down
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c SetPowerAction --action 0
```

## Notes

- The command uses IPMI chassis power control commands.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/setpoweraction.md