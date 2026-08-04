# ControlNvme

Locates, inserts, removes, or rescans an NVMe device.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ControlNvme --action <action> --dev_id <device ID> --group_id <group ID> --slot <slot number>
```

### In-Band
```
saa -c ControlNvme --action <action> --dev_id <device ID> --group_id <group ID> --slot <slot number>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ControlNvme --action <Action> --dev_id <device ID> --group_id <group ID> --slot <slot num>
```

## Actions

- **Locate**: Locates the device by turning on its LED light.
- **StopLocate**: Stops locating the device by turning off its LED light.
- **Insert**: Inserts the device.
- **Remove**: Removes the device.
- **Rescan**: Rescans the device. Only available on systems with TAS installed; does not require device ID, group ID, or slot parameters.

## Options

- `--action <action>`: Sets action to `1` = Locate, `2` = StopLocate, `3` = Insert, `4` = Remove, `5` = Rescan.
- `--dev_id`: The NVMe controller ID. Can be found using `GetNvmeInfo`.
- `--group_id`: The NVMe device group ID. Can be found using `GetNvmeInfo`.
- `--slot`: The NVMe slot number. Can be found using `GetNvmeInfo`.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.3.4 -u ADMIN -p PASSWORD -c ControlNvme --action Locate --dev_id 0 --group_id 0 --slot 0
[SAA_HOME]# ./saa -i 192.168.3.4 -u ADMIN -p PASSWORD -c ControlNvme --action Rescan
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ControlNvme --action Remove --dev_id 0 --group_id 0 --slot 1
[SAA_HOME]# ./saa -c ControlNvme --action Rescan
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ControlNvme --action Locate --dev_id 0 --group_id 0 --slot 0
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ControlNvme --action Rescan
```

## Notes

- Use `GetNvmeInfo` to retrieve the required parameters (device ID, group ID, and slot number). If using the `Rescan` action, no parameters are needed.
