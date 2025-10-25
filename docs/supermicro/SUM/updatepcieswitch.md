# UpdatePCIeSwitch

## Description

Use the "UpdatePCIeSwitch" command with the PCIe Switch firmware image to update the PCIe Switch firmware of a managed system.

## Syntax

```
sum -c UpdatePCIeSwitch --dev_id <index> --file <filename>
```

## Options

- `--dev_id <index>`: Specifies the device index of the PCIe Switch to update.
- `--file <filename>`: Specifies the PCIe Switch firmware image file.

## Examples

### In-Band
```
[SUM_HOME]# ./sum -c UpdatePCIeSwitch --file fw_file.img --dev_id 0
```

The console output contains the following information for a Broadcom chipset on an H12DGQ-NT6 system.

```
Managed system..........................localhost
PCIe Switch Device Vendor...............Broadcom
 Device ID(0)
 Device Name.........................SwitchPlx0
 Pex Cfg Version.....................1207
Local Firmware File......................H12DGQ_NT6_1209_PWR.bin
PCIe Switch Device Vendor................Broadcom
 Pex Cfg Version......................1209
```
