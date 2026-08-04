# UpdateMotherboardFpga

Updates the motherboard FPGA of a managed system with the given FPGA firmware image file. Used to run SAA on NVIDIA MGX&trade; systems to update the motherboard FPGA.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateMotherboardFpga --file <filename> --reboot
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateMotherboardFpga --file <filename> --reboot
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateMotherboardFpga --file <filename> --reboot
```

## Options

- `--file <file name>`: Updates the motherboard FPGA with the given FPGA image file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--individually` (Optional): Updates each motherboard FPGA with corresponding image file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateMotherboardFpga --file FPGA.bin --reboot
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateMotherboardFpga --file FPGA.bin --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateMotherboardFpga --file FPGA.bin --reboot
```

## Output

The execution progress for the managed system will be continuously updated to the "Execution Message" section of the managed system in the created log file.

## Notes

- During execution, DO NOT remove the AC power on the managed system.
- DO NOT flash BMC and BIOS firmware images at the same time.
- DO NOT update firmware image and configuration at the same managed system concurrently by in-band and OOB method.
