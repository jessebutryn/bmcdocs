# GetSystemInfo

Retrieves comprehensive firmware image information from the managed system. Without the `--redfish` option, this command provides a system-wide summary encompassing firmware details of components including System, LAN, BMC, BIOS, CPLD, SCP, and the Redfish version, if supported. With the `--redfish` option, it retrieves information on systems and chassis through the Redfish protocol.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSystemInfo [--redfish [--json_view [--file <SystemInfo.json> [--overwrite]]]]
```

### In-Band
```
saa [-I Redfish_HI [-u <username> -p <password>]] -c GetSystemInfo [--redfish [--json_view [--file <SystemInfo.json> [--overwrite]]]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSystemInfo [--redfish [--json_view [--file <SystemInfo.json> [--overwrite]]]]
```

## Options

- `--file <file name>`: Works with `--json_view` and saves the output to a file.
- `--overwrite`: Overwrites the output file.
- `--redfish`: (Optional) Enables support for pure Redfish.
- `--json_view`: (Optional) Shows the system information in JSON format.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c GetSystemInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -c GetSystemInfo -I Redfish_HI -u ADMIN -p ADMIN
```

### OOB
```bash
[SAA_HOME]# ./saa -c GetSystemInfo -i 10.168.29.116 -p ADMIN -u ADMIN

[SAA_HOME]# ./saa -c GetSystemInfo -i 10.168.29.116 -p ADMIN -u ADMIN --redfish

[SAA_HOME]# ./saa -c GetSystemInfo -i 10.168.29.116 -p ADMIN -u ADMIN --redfish --json_view

[SAA_HOME]# ./saa -c GetSystemInfo -i 10.168.29.116 -p ADMIN -u ADMIN --redfish --json_view --file SystemInfo.json --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSystemInfo
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

The execution progress for each managed system is continuously updated to the "Execution Message" section of that system in the created log file.

## Output

### Default (In-Band)
```
Managed system................localhost
 IPv4......................10.168.24.116
 BMC MAC address...........3A:EC:EF:CE:41:3B
 Firmware revision.........00.23.37
 Firmware build time.......2021/06/28
 BIOS version..............1.1
 BIOS build time...........06/21/2021
 CPLD version..............F0.09.46
 IPv6......................FE80:0000:0000:0000:AEEC:EFFF:FECE:413B/64
 System LAN1 MAC address...3A:EC:EF:CE:40:0F
 System LAN2 MAC address...3A:EC:EF:CE:40:A5
```

### Default (OOB, Redfish supported)
```
Managed system..................169.254.4.254
 IPv4........................10.168.24.116
 BMC MAC address.............3A:EC:EF:CE:41:3B
 Firmware revision...........00.23.37
 Firmware build time.........2021/06/28
 BIOS version................1.1
 BIOS build time.............06/21/2021
 CPLD version.................F0.09.46
 IPv6........................FE80:0000:0000:0000:AEEC:EFFF:FECE:413B/64
 System LAN1 MAC address.....3A:EC:EF:CE:40:0F
 System LAN2 MAC address.....3A:EC:EF:CE:40:A5
 Redfish version.............1.8.0
 Supermicro Redfish version..RF1.11-00.00

Managed system..................10.168.29.116
 IPv4........................10.168.29.116
 BMC MAC address.............3A:EC:EF:CE:41:3B
 Firmware revision...........00.23.37
 Firmware build time.........2021/06/28
 BIOS version................1.1
 BIOS build time.............06/21/2021
 CPLD version.................F0.09.46
 IPv6........................FE80:0000:0000:0000:AEEC:EFFF:FECE:413B/64
 System LAN1 MAC address.....3A:EC:EF:CE:40:0F
 System LAN2 MAC address.....3A:EC:EF:CE:40:A5
```

### --redfish
```
Redfish version.............1.8.0
Supermicro Redfish version..RF1.11-00.00
System information
===============================
[System]
 [System_0]
 Location:
 LocationType:
 ServiceLabel:
 Identify LED: Lit
 Serial number:
 Part number:
 Model:
 Asset tag:
 Manufacturer:
 Description: Computer System
 Sub model:
 System type: Physical
 Status (State): Disabled
 Power: PoweringOff
 Health: OK
 Health rollup:
 Memory summary
 Total system memory: 0 GiB
 Processor summary
 Count: 0
 Core count: 0
Chassis information
===============================
[BMC]
 [BMC_0]
 Location:
 LocationType: Embedded
 ServiceLabel:
 Identify LED: Lit
 Part number: AOM-SCM-NV2
 Serial number: $BOARD_SERIAL_NUMBER
 Model: BMC Secure Control Module
 Asset tag:
 Manufacturer: Supermicro
 Chassis type: Component
 Status (State): StandbyOffline
 Power: Off
 Health: OK
 Health rollup: OK
 Min power: 0 W
 Max power: 0 W
```

### --redfish --json_view --file
```
File "SystemInfo.json" is created.
```

## Notes

- The tables/elements returned may not be identical across managed systems; only tables/elements supported by the managed system are accessed.
