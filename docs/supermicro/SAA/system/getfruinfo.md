# GetFruInfo

Gets or dumps FRU (Field Replaceable Unit) information from the managed system, and can read FRU information from a local FRU file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetFruInfo [--file <filename> --dump [--format <file format>] [--overwrite]] [--dev_id <Device ID>] | [--showall]
saa -i <IP or host name> -u <username> -p <password> -c GetFruInfo [--file <filename> --dump [--format <file format>] [--overwrite]] [--redfish]
```

### In-Band
```
saa -c GetFruInfo [-I Redfish_HI [-u <username> -p <password>]] [--file <filename> {--dump [--format <file format>] [--overwrite] | --file_only}] [--dev_id <Device ID>] | [--showall]
saa -c GetFruInfo [-I Redfish_HI [-u <username> -p <password>]] [--file <filename> {--dump [--format <file format>] [--overwrite] | --file_only}] [--redfish]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetFruInfo [--file <filename> --dump [--format <file format>] [--overwrite]] [--dev_id <Device ID>] | [--showall]
saa -l <system list file> [-u <username> -p <password>] -c GetFruInfo [--file <filename> --dump [--format <file format>] [--overwrite]] [--redfish]
```

## Options

- `--file <file name>`: (Optional) Saves the dumped FRU data to a file.
- `--overwrite`: (Optional) Overwrites the output file.
- `--showall`: (Optional) Gets all FRU information from the managed system.
- `--file_only`: (Optional) Works with `--file`, and only reads FRU information from the input dumped FRU binary file.
- `--dump`: (Optional) Works with `--file`, and dumps FRU data.
- `--format <file format>`: (Optional) Works with `--file` and `--dump` to download FRU data to file in one of the following formats: `BINARY` (default) or `TEXT`.
- `--dev_id <Device ID>`: (Optional) Gets more FRUs from CMM. FRU ID: `[1-19]` or `ALL`:
    - `1` = CMM Master
    - `2` = CMM Middle Plane
    - `3` = CMM Switch(A1)
    - `4` = CMM Switch(A2)
    - `5` = CMM Switch(B1)
    - `6` = CMM Switch(B2)
    - `7` = CMM PSU(A1)
    - `8` = CMM PSU(A2)
    - `9` = CMM PSU(A3)
    - `10` = CMM PSU(A4)
    - `11` = CMM PSU(B1)
    - `12` = CMM PSU(B2)
    - `13` = CMM PSU(B3)
    - `14` = CMM PSU(B4)
    - `15` = CMM FAN(1)
    - `16` = CMM FAN(2)
    - `17` = CMM FAN(3)
    - `18` = CMM FAN(4)
    - `19` = CMM Slave
- `--redfish`: (Optional) Enables support for pure Redfish.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --dev_id 1,2

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --showall

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --file dumpedFile --dump --overwrite

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --file dumpedFile --dump --format TEXT --overwrite

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetFruInfo --file dumpedFile --dump --format BINARY --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetFruInfo --file dumpedFile --file_only

[SAA_HOME]# ./saa -c GetFruInfo

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetFruInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetFruInfo --file dumpedFile --dump

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetFruInfo --dev_id 1,2

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetFruInfo --showall
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If you execute `GetFruInfo` for 192.168.34.56 and 192.168.34.57, SAA creates `dumpedFile.192.168.34.56` and `dumpedFile.192.168.34.57`, respectively.

## Output

### CMM (--dev_id)
```
FRU information [Version=00.00]
===============================
 [CMM Master, ID=1, Size=256 bytes]
 Board mfg. Date/Time (BDT): 2022/08/17 13:49
 Board Manufacturer Name (BM): Supermicro
 Board Product Name (BPN): Chassis Management Module
 Board Serial Number (BS): UD22CS001903
 Board Part Number (BP): MBB-CMM-6
 Board Version (BV):
 Product Manufacturer (PM): Supermicro
 Product Name (PN): Chassis Management Module
 Product Part/Model Number (PPM): MBM-CMM-6
 Product Version (PV): 1.03
 Product Serial Number (PS):
 Product Asset Tag (PAT):
 [CMM Middle Plane, ID=2, Size=256 bytes]
 Board mfg. Date/Time (BDT): 2017/08/14 14:32
 Board Manufacturer Name (BM): Supermicro
 Board Product Name (BPN): MidPlane
 Board Serial Number (BS): GB197S006422
 Board Part Number (BP): BPN-SB-J820
 Product Manufacturer (PM): Supermicro
 Product Name (PN): MidPlane
 Product Part/Model Number (PPM): BPN-SB-J820
 Product Version (PV): 1.01A
 Product Serial Number (PS): GB197S006422
 Product Asset Tag (PAT):
```

### Dump to File
```
FRU information [Version=01.01]
===============================
 [BMC, ID=0, Size=256 bytes]
 Chassis Type (CT): 01
 Chassis Part Number (CP):
 Chassis Serial Number (CS):
 Board mfg. Date/Time (BDT): 1996/01/01 00:00
 Board Manufacturer Name (BM):
 Board Product Name (BPN):
 Board Serial Number (BS):
 Board Part Number (BP):
 Product Manufacturer (PM):
 Product Name (PN):
 Product Part/Model Number (PPM):
 Product Version (PV):
 Product Serial Number (PS):
 Product Asset Tag (PAT):
File "dumpedFile" is created
```

### In-Band (OOB / Redfish HI)
```
Chassis Type (CT): 01
Chassis Part Number (CP):
Chassis Serial Number (CS):
Board mfg. Date/Time (BDT): 2021/08/30 18:01
Board Manufacturer Name (BM): Supermicro
Board Product Name (BPN):
Board Serial Number (BS): WM218S011157
Board Part Number (BP):
Product Manufacturer (PM):
Product Name (PN):
Product Part/Model Number (PPM):
Product Version (PV):
Product Serial Number (PS):
Product Asset Tag (PAT):
FRU information [Version=00.00]
===============================
 [BMC, ID=0, Size=256 bytes]
 Chassis Type (CT): 00
 Chassis Part Number (CP):
 Chassis Serial Number (CS):
 Board mfg. Date/Time (BDT): 1996/01/01 00:00
 Board Manufacturer Name (BM):
 Board Product Name (BPN):
 Board Serial Number (BS):
 Board Part Number (BP):
 Product Manufacturer (PM):
 Product Name (PN):
 Product Part/Model Number (PPM):
 Product Version (PV):
 Product Serial Number (PS):
 Product Asset Tag (PAT):
```

## Notes

- The `--dev_id` option only supports CMM.
- The `--showall` option supports CMM and X13DEG-OAD.
- The FRU version is displayed if the managed system supports it.
