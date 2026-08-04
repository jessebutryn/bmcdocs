# CmmRotManage

Manages CMM Root of Trust (RoT) functions on RoT systems: retrieving CMM/backup/golden image information, updating the golden CMM image, recovering CMM, and downloading CMM evidence. Only supported on Blade systems with CMM AST2600.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CmmRotManage --action <action> [--file <evidence.bin.gz> [--overwrite]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CmmRotManage --action <action> [--file <evidence.bin.gz> [--overwrite]]
```

## Actions

- **GetInfo**: Retrieves information on active CMM, backed-up CMM, and golden CMM.
- **UpdateGolden**: Replaces the golden image with active CMM firmware.
- **Recover**: Recovers CMM from the backup image or the golden image. By priority, the managed system recovers CMM from the backup image; if the backup image is corrupted, it then recovers from the golden image.
- **DownloadEvidence**: Downloads CMM evidence. Only available after automatic or manual CMM recovery.

## Options

- `--action <action>`: Sets action to 1 = GetInfo, 2 = UpdateGolden, 3 = Recover, 4 = DownloadEvidence.
- `--file <file name>` (Optional): Works with `--action DownloadEvidence`. Saves the CMM evidence to a file.
- `--overwrite` (Optional): Works with `--action DownloadEvidence`. Overwrites the output file.
- `--redfish` (Optional): Enables pure Redfish support.

## Examples

### GetInfo
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CmmRotManage --action GetInfo
```

### DownloadEvidence
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CmmRotManage --action DownloadEvidence --file evidence.bin.gz
```

### UpdateGolden
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CmmRotManage --action UpdateGolden
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CmmRotManage --action UpdateGolden
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
 CMM version....................09.10.19
 Backup CMM version.............00.10.08
 Golden CMM version.............09.10.19
```

### DownloadEvidence
```
Start generating CMM evidence.
....................Done
Start downloading CMM evidence............Done
CMM evidence file "evidence.bin.gz" is created.
```

### UpdateGolden
```
Status: System is backing up current FW as golden image and CMM will be offline
for 6 minutes.
........................................
........................................
Done
Status: Please check Maintenance Event log for result.
```

## Notes

- This command is only supported on Blade systems with CMM AST2600.
- CMM will be disconnected while updating the golden image and recovering the firmware. Use the `GetMaintenEventLog` command to check the result afterwards.
- To execute `Recover` and `DownloadEvidence`, the SFT-DCMS-SINGLE license is required.
- This command is supported by OOB only.
- The `DownloadEvidence` action is only available after automatic or manual CMM recovery.
- The CMM evidence is a compressed gzip file.
