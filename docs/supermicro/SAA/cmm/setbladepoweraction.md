# SetBladePowerAction

Applies a power action to the whole Blade system, a single blade, or a specific node of a Blade system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetBladePowerAction --action <action> --blade <Blade Index> [--node <Node Index>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetBladePowerAction --action <action> --blade <Blade Index> [--node <Node Index>]
```

## Options

- `--action <action>`: Sets power action with:
  - `0` = down
  - `1` = up
  - `2` = cycle
  - `3` = reset
  - `4` = softshutdown
  - `24` = accycle
- `--blade [<Blade Index> | ALL]`: Assigns blade index. `[A1-A14]`, `[B1-B14]`, or `ALL`.
- `--node <Node Index>`: Assigns node index. `[1-4]` (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBladePowerAction --action down --blade ALL
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBladePowerAction --blade ALL --action reset
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBladePowerAction --blade A1 --action softshutdown
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBladePowerAction --action down --blade ALL
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBladePowerAction --blade ALL --action reset
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBladePowerAction --blade A1 --action softshutdown
```

## Notes

- To apply a power action to the whole Blade system, you only need to assign a power action.
- To apply a power action to a specific single Blade system, you must assign a power action and the `--blade` option with an index.
- To apply a power action to a specific node of a Blade system, you must assign a power action and both the `--blade` and `--node` options with indexes.
- If the execution Status field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
