# CpuPowerManage

Gets or sets the CPU power limit of the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CpuPowerManage --action <action> --value <value>
```

### In-Band
```
saa -c CpuPowerManage --action <action> --value <value>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CpuPowerManage --action <action> --value <value>
```

## Actions

- **GetPowerLimit** (`1`): Gets the current CPU power limit.
- **SetPowerLimitEnabled** (`2`): Enables and sets the CPU power limit.
- **SetPowerLimitDisabled** (`3`): Disables the CPU power limit.

## Options

- `--action <action>`: Sets action to `1` = GetPowerLimit, `2` = SetPowerLimitEnabled, `3` = SetPowerLimitDisabled.
- `--value <value>`: Assigns a power limit value.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CpuPowerManage --action GetPowerLimit

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CpuPowerManage --action SetPowerLimitEnabled --value 400
```

### In-Band
```bash
[SAA_HOME]# ./saa -c CpuPowerManage --action SetPowerLimitEnabled

[SAA_HOME]# ./saa -c CpuPowerManage --action SetPowerLimitEnabled --value 400
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CpuPowerManage --action GetPowerLimit
```

## Output

### GetPowerLimit (ARM system)
```
[ARM System]
 The CPU SoC power limit is 220 Watts.
```

### GetPowerLimit (AMD system)
```
[AMD System]
 The CPU Package Power Consumption is 42304 mWatts.
 The CPU SoC power limit is 240000 mWatts.
 The CPU SoC Max power limit is 240000 mWatts.
 The CPU current cTDP is 240000 mWatts.
 The CPU Max cTDP is 240000 mWatts.
 The CPU Min cTDP is 225000 mWatts.
```

### SetPowerLimitEnabled
```
.............................
The Cpu SoC power limit setting successfully.
```

## Notes

- If the Status field in the execution of the managed system shows SUCCESS, the console output of the managed system will be displayed in the Execution Message section of the log file created for the managed system.
