# UpdateUSBHostController

Updates the USB Host Controller firmware of a managed system using a USB Host Controller firmware image.

## Syntax

### Single System In-Band
```
saa -c UpdateUSBHostController {--dev_id <index>} {--file <fw_file_path>} [--cfg_file <cfg_file_path>] [--reboot]
```

### Remote In-Band
```
saa -c UpdateUSBHostController -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> {--dev_id <index>} {--file <fw_file_path>} [--cfg_file <cfg_file_path>] [--reboot] [--remote_saa <remote SAA path>]
```

### Multiple Systems Remote In-Band
```
saa -c UpdateUSBHostController -I Remote_INB -l <system list file> {--dev_id <index>} {--file <fw_file_path>} [--cfg_file <cfg_file_path>] [--reboot] [--remote_saa <remote SAA path>]
```

## Options

- `--dev_id <index>`: USB Host Controller device ID. Can be retrieved with the `GetUSBHostControllerInfo` command.
- `--file <fw_file_path>`: USB Host Controller firmware file.
- `--cfg_file <cfg_file_path>` (Optional): USB Host Controller configuration file.
- `--reboot` (Optional): Forces the managed system to power cycle after operation.
- `--remote_saa <remote SAA path>`: Path to the remote SAA executable (for remote in-band usage).

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c UpdateUSBHostController --dev_id 0 --file fw_file_path [--cfg_file cfg_file_path]
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
 Firmware File.......................K2024090.mem
 FW Version......................2.0.2.4
 Config File.........................cfg201v3.ini
 SubSystem Vendor ID.............FFFF
 SubSystem ID....................FFFF
Start to update firmware.
Erase Serial ROM completed.
Write Serial ROM completed.
Verify Serial ROM completed.
Update firmware successed.
Note: Please do power cycle to activate the updated image.
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
Start to update firmware.
Update firmware successed.
Note: Please do power cycle to activate the updated image.
```

## Notes

- Refer to the platform support table in `GetUSBHostControllerInfo` for supported chipsets/platforms.
- On the X14SBT-G platform with the Renesas USB Host Controller uPD720201 chipset, run `make -f Makefile.drv` in the `SAA/driver/renesas/USB` folder to build the device driver. The device driver build environment must have packages such as cmake and gcc installed.
