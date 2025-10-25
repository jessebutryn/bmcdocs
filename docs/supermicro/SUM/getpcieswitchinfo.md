# GetPCIeSwitchInfo

## Description

Use the "GetPCIeSwitchInfo" command to get and read the PCIe Switch information of the managed system and parse PCIe Switch information from the firmware file.

## Syntax

```
sum -c GetPCIeSwitchInfo [--file <filename> [--file_only]]
```

## Options

- `--file <filename>`: Specifies the firmware file to parse PCIe Switch information from.
- `--file_only`: Parses information only from the local file specified by --file.

## Examples

### In-Band
```
[SUM_HOME]# ./sum -c GetPCIeSwitchInfo
```

```
[SUM_HOME]# ./sum -c GetPCIeSwitchInfo --file fw_file.img --file_only
```

The console output contains the following information for the Broadcom chipset on the H12DGQ-NT6 system.

```
Managed system..........................localhost
PCIe Switch Device Vendor............... Broadcom
 Device ID(0)
 Device Name.........................SwitchPlx0
 Pex Cfg Version.....................1209
 Device ID(1)
 Device Name.........................SwitchPlx1
```
