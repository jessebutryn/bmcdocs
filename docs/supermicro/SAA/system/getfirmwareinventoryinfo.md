# GetFirmwareInventoryInfo

Retrieves comprehensive firmware inventory information from the managed system, providing a system-wide summary.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetFirmwareInventoryInfo [--json_view]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetFirmwareInventoryInfo [--json_view]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetFirmwareInventoryInfo [--json_view]
```

## Options

- `--json_view`: (Optional) Shows the firmware inventory information in JSON format.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFirmwareInventoryInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetFirmwareInventoryInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetFirmwareInventoryInfo
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

```
Managed system...............................192.168.34.56
 BMC......................................00.23.80
 BMC Backup...............................Not Present
 BMC Golden...............................00.23.69
 BMC Staging..............................00.23.80
 BIOS.....................................BIOS Date: 11/29/2023 Ver 1.8
 BIOS Backup..............................Not Present
 BIOS Golden..............................BIOS Date: 07/12/2022 Ver 1.4
 BIOS Staging.............................BIOS Date: 11/29/2023 Ver 1.8
 CPLD Motherboard.........................F0.09.46
 BIOS ME..................................4.4.4.603

Managed system...............................169.254.3.254
 BMC......................................00.23.80
 BMC Backup...............................Not Present
 BMC Golden...............................00.23.69
 BMC Staging..............................00.23.80
 BIOS.....................................BIOS Date: 11/29/2023 Ver 1.8
 BIOS Backup..............................Not Present
 BIOS Golden..............................BIOS Date: 07/12/2022 Ver 1.4
 BIOS Staging.............................BIOS Date: 11/29/2023 Ver 1.8
 CPLD Motherboard.........................F0.09.46
 BIOS ME..................................4.4.4.603
```

## Notes

- Executing `GetFirmwareInventoryInfo` with the `--json_view` option shows the firmware inventory information in JSON format.
