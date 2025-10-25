# GetFruInfo

## Description

Use the "GetFruInfo" command to get or dump FRU information on the managed system and read FRU information from the local FRU file.

## Notes

- The "--dev_id" option only supports CMM.
- The "--showall" option can support CMM and X13DEG-OAD.

## Syntax

```
sum [-i <IP or host name>] -u <username> -p <password> -c GetFruInfo [--file <filename> [--dump] | [--file_only]] [--overwrite] [--dev_id <Device ID>] | [--showall]
```

## Options

- `--file <filename>`: Specifies the file to save or read FRU information.
- `--dump`: Dumps FRU information to the file.
- `--file_only`: Reads FRU information from the local file only.
- `--overwrite`: Overwrites the output file if it exists.
- `--dev_id <Device ID>`: Specifies the device ID (only supports CMM).
- `--showall`: Shows all FRU information (supports CMM and X13DEG-OAD).

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --file dumpedFile --dump --overwrite
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --dev_id 1,2
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --showall
The console output contains the following information:
FRU information
===================
 [CMM Master]
 Mfg. Date: 2017/04/05 11:35
 Board Manufacturer: Supermicro
 Board Product Name: Chassis Management Module
 Board Serial Number:
 Board Part Number: MBB-CMM-003
 Manufacturer Name: Supermicro
 Product Name: Chassis Management Module
 Product Part Number: MBM-CMM-003
 Product Version: 1
 Product Serial Number:
 Asset Tag:
 [CMM Middle Plane]
 Mfg. Date: 2017/10/30 14:24
 Board Manufacturer: Supermicro
 Board Product Name: MidPlane
 Board Serial Number: GB196S006132
 Board Part Number: BPN-SB-J610
 Manufacturer Name: Supermicro
 Product Name: MidPlane
 Product Part Number: BPN-SB-J610
 Product Version: 1.00
 Product Serial Number: GB196S006132
 Asset Tag:
```

### In-Band
```
[SUM_HOME]# ./sum -c GetFruInfo --file dumpedFile --file_only
The console output contains the following information:
Mfg. Date: 2021/08/30 18:01
Board Manufacturer: Supermicro
Board Product Name:
Board Serial Number: WM218S011157
Board Part Number:
Manufacturer Name:
Product Name:
Product Part Number:
Product Version:
```
