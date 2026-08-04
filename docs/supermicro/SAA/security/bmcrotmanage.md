# BmcRotManage

Manages BMC Root of Trust (RoT) functions on RoT systems: retrieving BMC/backup/golden image information, updating the golden BMC image, recovering BMC, and downloading BMC evidence.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BmcRotManage --action <action> [--file <evidence.bin.gz> [--overwrite]]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c BmcRotManage --action <action> [--file <evidence.bin.gz> [--overwrite]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BmcRotManage --action <action> [--file <evidence.bin.gz> [--overwrite]]
```

## Actions

- **GetInfo**: Retrieves information on active BMC, backed-up BMC, and golden BMC.
- **UpdateGolden**: Replaces the golden image with active BMC firmware.
- **Recover**: Recovers BMC from the backup image or the golden image. By priority, the managed system recovers BMC from the backup image; if the backup image is corrupted, it then recovers from the golden image.
- **DownloadEvidence**: Downloads BMC evidence. Only available after automatic or manual BMC recovery.

## Options

- `--action <action>`: Sets action to 1 = GetInfo, 2 = UpdateGolden, 3 = Recover, 4 = DownloadEvidence.
- `--file <file name>` (Optional): Works with `--action DownloadEvidence`. Saves the BMC evidence to a file.
- `--overwrite` (Optional): Works with `--action DownloadEvidence`. Overwrites the output file.
- `--redfish` (Optional): Enables support for pure Redfish.

## Examples

### GetInfo (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcRotManage --action GetInfo
```

### DownloadEvidence (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcRotManage --action DownloadEvidence --file evidence.bin.gz
```

### UpdateGolden (In-Band through Redfish Host Interface)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c BmcRotManage --action UpdateGolden
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BmcRotManage --action UpdateGolden
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### GetInfo
```
Managed system.....................192.168.34.56
 BMC version....................09.10.19
 Backup BMC version.............00.10.08
 Golden BMC version.............09.10.19
```

### UpdateGolden
```
Status: System is backing up current FW as golden image and BMC will be offline
for 6 minutes.
........................................
........................................
Done
Status: Please check Maintenance Event log for result.
```

### DownloadEvidence
```
Start generating BMC evidence.
....................Done
Start downloading BMC evidence............Done
BMC evidence file "evidence.bin.gz" is created.
```

## Notes

- BMC will be disconnected while updating the golden image and recovering the firmware. Use the `GetMaintenEventLog` command to check the result afterwards.
- To execute `Recover` and `DownloadEvidence`, the SFT-DCMS-SINGLE license is required.
- This command is supported by OOB use; in-band usage is restricted to the Redfish host interface.
- The `DownloadEvidence` action is only available after automatic or manual BMC recovery.
- The BMC evidence is a compressed gzip file.
