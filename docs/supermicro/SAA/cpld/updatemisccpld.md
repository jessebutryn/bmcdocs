# UpdateMiscCpld

Updates the motherboard Miscellaneous CPLD of a managed system on NVIDIA MGX™ systems, using the given CPLD firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateMiscCpld --file <filename> --reboot
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateMiscCpld --file <filename> --reboot
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateMiscCpld --file <filename> --reboot
```

## Options

- `--file <file name>`: Updates the motherboard Miscellaneous CPLD with the given CPLD image file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--individually`: (Optional) Updates each motherboard Miscellaneous CPLD with its corresponding image file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateMiscCpld --file MISC_CPLD.jed --reboot
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateMiscCpld --file MISC_CPLD.jed --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateMiscCpld --file MISC_CPLD.jed --reboot
```

## Output

The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
