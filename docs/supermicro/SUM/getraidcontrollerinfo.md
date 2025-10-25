# GetRaidControllerInfo

## Description

Use the "GetRaidControllerInfo" command to get the RAID firmware image information from the managed system or the RAID firmware image.

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c GetRaidControllerInfo [--file <filename> [--file_only]] [--controller <Broadcom or Marvell>] [--dev_id <controller_id>]
```

## Options

- `--file <filename>`: Specifies the RAID firmware image file to read information from.
- `--file_only`: Reads information only from the local file specified by --file.
- `--controller <Broadcom or Marvell>`: Specifies the controller type.
- `--dev_id <controller_id>`: Specifies the device ID of the controller.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetRaidControllerInfo --file RAID.rom
```

### In-Band
```
[SUM_HOME]# ./sum -c GetRaidControllerInfo --file RAID.rom
```

```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c GetRaidControllerInfo --file RAID.rom --controller Broadcom --dev_id 0
The console output contains the following information.
Managed System........................ 192.168.34.56
Device ID............................. Device 0
Product Name.......................... AVAGO 3108 MegaRAID
Serial................................ N/A
Package............................... 24.18.0-0021
Firmware Version...................... 4.670.00-6500
BIOS Version.......................... 6.34.01.0_4.19.08.00_0x06160200
Boot Block Version.................... 3.07.00.00-0003
Local RAID Firmware Image File........ AVAGO_3108_4.680.00-8290.rom
Product Name.......................... AVAGO 3108 MegaRAID
Package............................... 24.21.0-0028
Firmware Version...................... 4.680.00-8290
BIOS Version.......................... 6.36.00.2_4.19.08.00_0x06180202
Boot Block Version.................... 3.07.00.00-0003
```

```
[SUM_HOME]# ./sum -c GetRaidControllerInfo --file RAID.rom --file_only
The console output contains the following information.
Local RAID Firmware Image File........ AVAGO_3108_4.680.00-8290.rom
Product Name.......................... AVAGO 3108 MegaRAID
Package............................... 24.21.0-0028
Firmware Version...................... 4.680.00-8290
BIOS Version.......................... 6.36.00.2_4.19.08.00_0x06180202
Boot Block Version.................... 3.07.00.00-0003
```

## Notes

- For X11 platforms, the "GetRaidControllerInfo" command only supports Broadcom 3108.
- For X12 and later platforms, the "GetRaidControllerInfo" command only supports Broadcom 3108, 3808, 3816, 3908, 3916, and Marvell SE9230.
