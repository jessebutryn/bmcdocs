# SecureEraseRaidHdd

Securely erases hard disks (HDD or SSD) attached to a target RAID controller system, and polls the erasing status asynchronously or synchronously. Supported on X12/H12 and later platforms.

## Syntax

### OOB (Pre-check)
```
saa -i <IP or host name> -u <username> -p <password> -c SecureEraseRaidHdd --precheck
```

### OOB (Erase)
```
saa -i <IP or host name> -u <username> -p <password> -c SecureEraseRaidHdd --dev_id <device_id> [--enc_id <enclosure id>] [--dsk_id <disk id>] [--sync] [--type <BRCM_IT|BRCM_IR>]
```

### OOB (Poll Task Status)
```
saa -i <IP or host name> -u <username> -p <password> -c SecureEraseRaidHdd --tsk_id <task id> [--sync]
```

### OOB (Abort)
```
saa -i <IP or host name> -u <username> -p <password> -c SecureEraseRaidHdd --dev_id <device_id> [--enc_id <enclosure id>] [--dsk_id <disk id>] [--abort]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c SecureEraseRaidHdd [--dev_id <device_id> [--enc_id <enclosure id>] [--dsk_id <disk id>] [--sync] [--type <BRCM_IT|BRCM_IR>]] | --precheck
saa -I Redfish_HI -u <username> -p <password> -c SecureEraseRaidHdd --tsk_id <task id> [--sync]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SecureEraseRaidHdd [--dev_id <device_id> [--enc_id <enclosure id>] [--dsk_id <disk id>] [--sync] [--type <BRCM_IT|BRCM_IR>]] | --precheck
saa -l <system list file> [-u <username> -p <password>] -c SecureEraseRaidHdd --tsk_id <task id> [--sync]
```

## Options

- `--dev_id <Device ID>`: A RAID controller ID for secure erase.
- `--enc_id <Enclosure ID>`: Enclosure ID list or "ALL" in the RAID controller for secure erase.
- `--dsk_id <Disk ID>`: Disk ID list or "ALL" in the RAID controller for secure erase.
- `--tsk_id <Task ID>` (Optional): Accesses the progress of a secure erase.
- `--precheck` (Optional): Displays detailed information for the list of the RAID controller (model, manufacturer and ID of RAID card, enclosure ID, disk ID, F/W state, and Secure-Erase support on each disk).
- `--abort` (Optional): Stops the list of RAID controller secure erase actions.
- `--sync` (Optional): Shows the current progress of the secure-erase operation of the RAID controller.
- `--type <BRCM_IT|BRCM_IR>` (Optional): Specifies the RAID controller mode.

## Examples

### Pre-check
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --precheck
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --precheck
```

### Erase
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --dev_id 0 --enc_id 0,1 --dsk_id 0,1,2,3
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --dev_id 0 --enc_id 0,1,2 --dsk_id 0,3,4
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --dev_id 0 --enc_id ALL --dsk_id ALL --sync
```

### Erase with Synchronous Polling
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --dev_id 0 --enc_id ALL --dsk_id 0,1,2,3 --sync
```

### Poll Task Status
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --tsk_id 1,2,3,4,5,6 --sync
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --tsk_id 1,2,3
```

### Abort
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --dev_id 0 --enc_id 0 --dsk_id 2,3 --abort
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SecureEraseRaidHdd --dev_id 0 --enc_id ALL --dsk_id 0,1,2 --abort
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### --precheck
```
 Dev_ID Enc_ID Dsk_ID Manufacturer Model FW Status Support Erase Status
 ------ ------ ------ ------------ ----------- ------------------------- ---------------
 0 0 0 Broadcom SAS 3808 Unconfigured good drive Yes
 0 0 1 Broadcom SAS 3808 Unconfigured good drive Yes
 0 0 2 Broadcom SAS 3808 Unconfigured good drive Yes
```

### Erase (F/W state check and response)
```
Warning: Please make sure the F/W State of each disk is in "Unconfigured good drive"
Otherwise, please
1 Delete your virtual disk(VD) if any.
Or
(2) Disable JBOD mode if set before.
Checking FW state of each disk...
The F/W STATE of EACH DISK :
[--dev_id:--enc_id:--dsk_id] : F/W State
[ 0: 0: 0] : Unconfigured good drive
[ 0: 0: 1] : Unconfigured good drive
[ 0: 0: 2] : Configured-drive is online
[ 0: 0: 3] : Configured-drive is online
****************************<<<<<ERROR>>>>>*****************************
 ExitCode = 153
 Description = IPMI execution on non-supported device
 Program Error Code = 440.21
 Error message:
 The F/W state:
 Enclosure ID: 0 Disk ID: 2
 Enclosure ID: 0 Disk ID: 3
 are not allowed to be securely erased.
 Instruction:
 Please check the F/W state of unallowed disks and try again.
```

### Erase with --sync (task IDs assigned and progress polling)
```
SECURE ERASE RESPONSE :
[--dev_id:--enc_id:--dsk_id:--tsk_id] : MESSAGE
[ 0: 0: 0: 1] : Already started polling progress.
[ 0: 0: 1: 2] : Already started polling progress.
[ 0: 0: 2: 3] : Start polling progress.
[ 0: 0: 3: 4] : Start polling progress.
[ 0: 1: 0: 5] : Start polling progress.
[ 0: 1: 1: 6] : Start polling progress.
Secure-Erase progress is starting...
-------------------------RAID Controller Task Service-------------------------
Tsk | RAID | Enc | Dsk | Progress | State | Start Time | Elapsed |
1 | 0 | 0 | 0 | 72% | Running | 12:53:43 | |
2 | 0 | 0 | 1 | 73% | Running | 12:54:17 | |
3 | 0 | 0 | 2 | 4% | Running | 14:32:47 | |
4 | 0 | 0 | 3 | 4% | Running | 14:32:55 | |
5 | 0 | 1 | 0 | 4% | Running | 14:33:17 | |
6 | 0 | 1 | 1 | 4% | Running | 14:33:25 | |
Polling progress...
```

### Poll Task Status (completed)
```
-------------------------RAID Controller Task Service-------------------------
Tsk | RAID | Enc | Dsk | Progress | State | Start Time | Elapsed |
 1 | 0 | 0 | 0 | 100% | Completed | 12:53:43 | 02:44:13 |
 2 | 0 | 0 | 1 | 100% | Completed | 12:54:17 | 02:44:13 |
 3 | 0 | 0 | 2 | 100% | Completed | 14:32:47 | 02:45:13 |
 4 | 0 | 0 | 3 | 100% | Completed | 14:32:55 | 02:45:13 |
 5 | 0 | 1 | 0 | 100% | Completed | 14:33:17 | 02:46:13 |
 6 | 0 | 1 | 1 | 100% | Completed | 14:33:25 | 02:46:13 |
Secure-Erase progress Done.
```

### Abort
```
Checking F/W state of each disk...
The F/W STATE of EACH DISK :
[--dev_id:--enc_id:--dsk_id] : F/W State
[ 0: 0: 2] : Unconfigured good drive
[ 0: 0: 3] : Unconfigured good drive
Start aborting securely erasing each disk...
.......Finish aborting Secure-Erase progress.
```

### Abort (failure)
```
****************************<<<<<ERROR>>>>>*****************************
 ExitCode = 120
 Description = Invalid Redfish response
 Program Error Code = 440.24
 Error message:
 The following disk list fail to abort for Secure Erase action.
 The list format is [--dev_id:--enc_id:--dsk_id]
 1. [0:0:1]
```

## Notes

- This command is supported on X12/H12 and later platforms.
- Before erasing, use `GetRaidCfg` to confirm the JBOD mode of the RAID controller system is "Disabled," and that the disks to be erased are in "Unconfigured good drive" state. Use `--precheck` to see model, manufacturer, ID, enclosure ID, disk ID, F/W state, and Secure-Erase support for each disk.
- If a target disk is accepted for secure erase or is being securely erased, a task ID is returned; remember the task ID(s) for polling status. If a disk is not allowed for secure erase, there is no task ID.
- Poll erasing status immediately by appending `--sync` to the initial erase command, or later using `--tsk_id`.
- In multiple systems, the `--sync` option is not allowed with `--tsk_id` for polling the erasing status on the RAID controller system.
- The Secure-Erase function for IT/HBA RAID controllers is supported by OEM FW only.
- For Windows, argument values can be quoted or unquoted, e.g. `--enc_id "ALL"` or `--enc_id ALL`.
- Supported RAID cards include: AOC-S3108L-H8iR(-16DD), AOC-SLG3-2H8M2, AOC-S3808L-L8iR, AOC-S3816L-L16iR, AOC-S3908L-H8iR(-16DD/-32DD), AOC-S3916L-H16iR(-32DD), AOC-S3808L-L8iT1, AOC-S3816L-L16iT1, AOC-SLG4-2H8M2, AOC-SMG4-2M2, AOC-SMG4-2E1S, AOM-S3808NI-4NM, AOM-M3808NI-4HM.
