# BiosRotManage

Manages BIOS Root of Trust (RoT) functions on RoT systems: retrieving BIOS/backup/golden image information, updating the golden BIOS image, recovering BIOS, and downloading BIOS evidence.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BiosRotManage --action <action> [--redfish] [--file <evidence.bin.gz> [--overwrite]] [--reboot]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c BiosRotManage --action <action> [--file <evidence.bin.gz> [--overwrite]] [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BiosRotManage --action <action> [--redfish] [--file <evidence.bin.gz> [--overwrite]] [--reboot]
```

## Actions

- **GetInfo**: Retrieves information on active BIOS, backed-up BIOS, and golden BIOS.
- **UpdateGolden**: Replaces the golden image with an active BIOS image.
- **Recover**: Recovers BIOS from the backup image or the golden image. By priority, the managed system recovers BIOS from the backup image; if the backup image is corrupted, it then tries to recover from the golden image.
- **DownloadEvidence**: Downloads BIOS evidence. Only available after automatic or manual BIOS recovery.

## Options

- `--action <action>`: Sets action to 1 = GetInfo, 2 = UpdateGolden, 3 = Recover, 4 = DownloadEvidence.
- `--file <file name>` (Optional): Works with `--action DownloadEvidence`. Saves the BIOS evidence to a file.
- `--overwrite` (Optional): Works with `--action DownloadEvidence`. Overwrites the output file.
- `--reboot` (Optional): Works with `--action UpdateGolden` and `Recover`. Forces the managed system to reboot or power up after operation.
- `--redfish` (Optional): Enables pure Redfish support.
- `--post_complete` (Optional): Waits for the managed system's POST to complete after reboot.

## Examples

### GetInfo (In-Band through Redfish Host Interface)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c BiosRotManage --action GetInfo
```

### UpdateGolden (OOB)
```bash
[SAA_HOME]# ./saa -I 192.168.34.56 -u ADMIN -p PASSWORD -c BiosRotManage --action UpdateGolden --reboot
```

### DownloadEvidence (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BiosRotManage --action DownloadEvidence --file evidence.bin.gz
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BiosRotManage --action UpdateGolden --reboot
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### GetInfo
```
Managed system.....................169.254.3.254
 BIOS build date................2022/10/24 Ver 1.0a
 Backup BIOS build date.........2022/10/24 Ver 1.0a
 Golden BIOS build date.........2022/10/24 Ver 1.0a
```

### UpdateGolden
```
Note: System will be powered off shortly to continue the process. Please wait for
the system to power on again, then check the Maintenance Event log for results.
Warning: Please wait for the system to power on again. Do not remove AC power
before the system reboots.
..................................................
..................................................
..................................................
.............
.....
```

### DownloadEvidence
```
Start generating BIOS evidence.
....................Done
Start downloading BIOS evidence..........Done
BIOS evidence file "evidence.bin.gz" is created.
```

## Notes

- To execute `UpdateGolden` or `Recover`, it is necessary to power off the system, which requires the `--reboot` option. Use the `GetMaintenEventLog` command to check the results after the system is powered on.
- To execute `Recover` and `DownloadEvidence`, the SFT-DCMS-SINGLE license is required.
- This command is supported by OOB use; in-band usage is restricted to the Redfish host interface only.
- The `DownloadEvidence` action is only available after automatic or manual BIOS recovery.
- The BIOS evidence is a compressed gzip file.
