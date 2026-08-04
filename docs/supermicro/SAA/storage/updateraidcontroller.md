# UpdateRaidController

Updates the RAID controller firmware on the managed system with the given RAID firmware image file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateRaidController --file <filename> --controller <Broadcom|Marvell> [--type <HBA|HA-RAID>] --dev_id <controller_id> [--upgrade_only] [{[--reboot] | [--check_reboot_required]}]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c UpdateRaidController --file <filename> --controller <Broadcom|Marvell> [--type <HBA|HA-RAID>] --dev_id <controller_id> [--upgrade_only] [{[--reboot] | [--check_reboot_required]}]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateRaidController --file <filename> --controller <Broadcom|Marvell> [--type <HBA|HA-RAID>] --dev_id <controller_id> [--upgrade_only] [{[--reboot] | [--check_reboot_required]}]
```

## Options

- `--file <file name>`: Updates the RAID controller with the given RAID image file.
- `--controller <Controller>`: Vendor of the RAID controller — `Broadcom` or `Marvell`.
- `--type <Type>`: Specifies RAID type for Broadcom devices. Supported types: `HBA`, `HA-RAID`.
- `--dev_id <Device ID>`: Device ID of the RAID controller.
- `--reboot`: Forces the managed system to reboot or power up after operation (optional).
- `--post_complete`: Waits for the managed system's POST to complete after reboot (optional).
- `--upgrade_only`: Firmware updates are only performed when the version is newer (optional).
- `--check_reboot_required`: Displays a warning message when a system reboot or power cycle is required (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateRaidController --controller Broadcom --type HA-RAID --dev_id 0 --file RAID.rom --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateRaidController --controller Marvell --dev_id 0 --file RAID.rom --upgrade_only --reboot --post_complete
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateRaidController --controller Broadcom --type HA-RAID --dev_id 0 --file RAID.rom --upgrade_only --check_reboot_required
```

## Notes

- Supported RAID controllers:
  - Broadcom: 3108, 3408, 3808, 3808N (AOM-S3808NI-4NM, AOC-SMG4-2M2, AOM-M3808NI-4HM), 3816, 3908, 3916, 4116.
  - Marvell: SE9230, 88NR2241.
- The Broadcom 3108 RAID controller is supported starting with RAID firmware image version 4.650.00-8095 and later.
- Starting with X12 platforms and later, the `--type` option is required when using the Broadcom controller.
- The Marvell 88NR2241 RAID controller does not support the `--upgrade_only` option, since the firmware version in the Marvell 88NR2241 firmware image cannot be retrieved.
