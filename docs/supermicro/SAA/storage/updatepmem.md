# UpdatePMem

Updates the PMem firmware of the managed system with the given PMem firmware image, or restores the BIOS built-in PMem firmware.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdatePMem {--file <filename> | --restore_default_fw} [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdatePMem --file <filename> [--reboot]
saa -c UpdatePMem --restore_default_fw [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdatePMem {--file <filename> | --restore_default_fw} [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]]
```

## Options

- `--file <file name>`: Updates the PMem with the given PMem firmware file (optional).
- `--reboot`: Forces the managed system to reboot or power up after operation (optional).
- `--restore_default_fw`: Updates the PMem with the BIOS built-in PMem firmware (optional).
- `--current_password <current password>`: Checks the current BIOS Administrator password (optional).
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password (optional).
- `--post_complete`: Waits for the managed system's POST to complete after reboot (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePMem --file PMem.bin --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePMem --index all --reboot --post_complete
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdatePMem --file PMem.bin --reboot

[SAA_HOME]# ./saa -c UpdatePMem --restore_default_fw --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdatePMem --file PMem.bin --reboot
```

## Output

```
Managed system................192.168.34.56
 PMem version..............2.2.0.1464
Local PMem image file.....Supermicro_PSU.x0
 PMem version..............2.2.0.1469
Status: Start uploading PMem firmware for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Status: PMem firmware is updated for 192.168.34.56
Status: The managed system 192.168.34.56 is rebooting.
.........................Done
Status: PMem is updated for 192.168.34.56
WARNING: Without option --post_complete, please manually confirm the managed
system is POST complete before executing next action.
```

## Notes

- This command is available on X12 3rd Gen Intel Xeon Scalable processors with Intel C621A Series Chipsets and later platforms.
- For more detailed usage of PMem, contact Supermicro technical support.
- The execution progress for the managed system will be continuously updated to the Execution Message section of the created log file.
