# GpuPowerManage

Gets or sets the GPU power limit of the managed system.

## Syntax

### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GpuPowerManage --item <item name> --action <action> --dev_id <id> --value <value>
```

### Single System In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GpuPowerManage --item <item name> --action <action> --dev_id <id> --value <value>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GpuPowerManage --item <item name> --action <action> --dev_id <id> --value <value>
```

## Actions

- **GetPowerLimit**: Gets the current GPU power limit.
- **SetPowerLimit**: Sets the GPU power limit.

## Options

- `--item <item name>`: Item type of GPU. Value: `1 = HGX`.
- `--action <action>`: Sets action to GetPowerLimit or SetPowerLimit.
- `--dev_id <Device ID List>`: GPU SXM Device ID; can consist of multiple numbers, ranging from 1 to 8 (separated by comma), or `All`.
- `--value <Value>`: Assigns the power limit value.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GpuPowerManage --item HGX --action GetPowerLimit --dev_id 1,2,3

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GpuPowerManage --item HGX --action SetPowerLimit --dev_id 1,2,3 --value 700
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GpuPowerManage --item HGX --action SetPowerLimit --dev_id all

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GpuPowerManage --item HGX --action SetPowerLimit --dev_id all --value 700
```

## Output

```
[GPU SXM 1]
 Power Limit Max value: 700
 Power Limit Min value: 200
 Power Limit Current value: 700
[GPU SXM 2]
 Power Limit Max value: 700
 Power Limit Min value: 200
 Power Limit Current value: 700
[GPU SXM 3]
 Power Limit Max value: 700
 Power Limit Min value: 200
 Power Limit Current value: 700
```

## Notes

- If the "Status" field in the execution of the managed system shows SUCCESS, the console output of the managed system will be displayed in the "Execution Message" section of the log file created for the managed system.
