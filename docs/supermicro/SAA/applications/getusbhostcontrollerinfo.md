# GetUSBHostControllerInfo

Gets and reads the USB Host Controller information of the managed system, and parses USB Host Controller information from firmware and configuration files.

## Syntax

### Single System In-Band
```
saa -c GetUSBHostControllerInfo [--file <filename> --cfg_file <cfgfilename> [--file_only]]
```

### Remote In-Band
```
saa -c GetUSBHostControllerInfo -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> [--remote_saa <remote SAA path>]
```

### Multiple Systems Remote In-Band
```
saa -c GetUSBHostControllerInfo -I Remote_INB -l <system list file> [--remote_saa <remote SAA path>]
```

## Options

- `--file <filename>`: Reads the USB Host Controller information from an input firmware file.
- `--cfg_file <cfgfilename>`: Reads the USB Host Controller information from an input configuration file.
- `--file_only`: Works with `--file`/`--cfg_file`, and only reads USB Host Controller information from the input file(s).
- `--remote_saa <remote SAA path>`: Path to the remote SAA executable (for remote in-band usage).

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c GetUSBHostControllerInfo

[SAA_HOME]# ./saa -c GetUSBHostControllerInfo --file fw_file_path --file_only

[SAA_HOME]# ./saa -c GetUSBHostControllerInfo --cfg_file cfg_file_path --file_only
```

## Output

### Renesas uPD720201 Chipset (X14SBT-G)
```
Managed system..........................localhost
 Device ID(0)
 Address(Bus-Dev-Func)...........15-00-00
 FW Version......................2.0.2.6
 Revision........................3
 PCI Subsystem ID................FFFF
 PCI Subsystem Vendor ID.........FFFF
 Device ID(1)
 Address(Bus-Dev-Func)...........18-00-00
 FW Version......................2.0.2.6
 Revision........................3
 PCI Subsystem ID................FFFF
 PCI Subsystem Vendor ID.........FFFF
 Firmware File.......................K2024090.mem
 FW Version......................2.0.2.4
 Config File.........................cfg201v3.ini
 SubSystem Vendor ID.............FFFF
 SubSystem ID....................FFFF
```

### ASMedia ASM3042 Chipset (X14SBH)
```
Managed system..........................localhost
 Device ID(0)
 Bus.............................0x3B
 Device..........................0x00
 Function........................0x00
 FW Version......................230802_71_02_40
 PCI Subsystem ID................1d48
 PCI Subsystem Vendor ID.........15d9
 Firmware File.......................230802_71_1F_42.bin
 FW Version......................230802_71_1f_42
 SubsyetemID.....................N/A
 SubsyetemVendorID...............N/A
```

## Notes

- This command is available on the following platforms:

| Platform | Chipset | Supported OS |
|---|---|---|
| X14SBT-G | Renesas uPD720201 | Ubuntu 20.04 and later, Red Hat 9.0 and later |
| X14SBH | ASMedia ASM3042 | Ubuntu 20.04 and later, Red Hat 9.0 and later, Windows Server |
