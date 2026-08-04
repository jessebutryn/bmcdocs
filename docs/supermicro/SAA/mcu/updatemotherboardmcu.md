# UpdateMotherboardMcu

Updates the motherboard MCU of a managed system with the given MCU firmware image file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateMotherboardMcu --file <filename> --reboot [--post_complete]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateMotherboardMcu --file <filename> --reboot
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateMotherboardMcu --file <filename>
```

## Options

- `--file <file name>`: Updates the motherboard MCU with the given image file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `-I Redfish_HI` (Optional): Uses Redfish Host Interface to query the firmware information. (Only in-band usage is supported.)
- `--post_complete` (Optional): Waits for the managed system POST to complete after reboot.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateMotherboardMcu --file MBD_MCU.bin --reboot --post_complete
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateMotherboardMcu --file MBD_MCU.bin --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateMotherboardMcu --file MBD_MCU.bin
```

## Output

The execution progress for the managed system will be continuously updated to the "Execution Message" section of the managed system in the created log file.

## Notes

- During execution, DO NOT remove the AC power on the managed system.
- DO NOT flash BMC and BIOS firmware images at the same time.
- DO NOT update firmware image and configuration at the same managed system concurrently by in-band and OOB method.
