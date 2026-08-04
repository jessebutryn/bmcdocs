# GetRaidControllerInfo

Gets the RAID controller firmware image information from the managed system, as well as information from a local RAID firmware image file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetRaidControllerInfo [--file <filename>] [--controller <Broadcom|Marvell>] [--dev_id <controller_id>]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetRaidControllerInfo [--file <filename> [--file_only]] [--controller <Broadcom|Marvell>] [--dev_id <controller_id>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetRaidControllerInfo [--file <filename>] [--controller <Broadcom|Marvell>] [--dev_id <controller_id>]
```

## Options

- `--file <file name>`: Reads the RAID controller firmware information from an input RAID image file (optional).
- `--controller <Controller>`: Vendor of the RAID controller — `Broadcom` or `Marvell` (optional).
- `--dev_id <Device ID>`: RAID controller device ID.
- `--file_only`: Works with `--file`, and only reads RAID controller information from the input image file (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetRaidControllerInfo --file RAID.rom
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetRaidControllerInfo --file RAID.rom

[SAA_HOME]# ./saa -c GetRaidControllerInfo --file RAID.rom --file_only
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetRaidControllerInfo --file RAID.rom
```

## Output

```
 Managed System........................192.168.34.56
 Device ID.............................Device 0
 Product Name..........................AVAGO 3108 MegaRAID
 Serial................................N/A
 Package...............................24.18.0-0021
 Firmware Version......................4.670.00-6500
 BIOS Version..........................6.34.01.0_4.19.08.00_0x06160200
 Boot Block Version....................3.07.00.00-0003
 Local RAID Firmware Image File........AVAGO_3108_4.680.00-8290.rom
 Product Name..........................AVAGO 3108 MegaRAID
 Package...............................24.21.0-0028
 Firmware Version......................4.680.00-8290
 BIOS Version..........................6.36.00.2_4.19.08.00_0x06180202
 Boot Block Version....................3.07.00.00-0003
```

## Notes

- Use the `BladeSummary` command to check Blade ID and Node ID within CMM.
- If the execution Status field for a managed system is SUCCESS, the RAID information of the managed system will be shown in the Execution Message section of the created log file.
