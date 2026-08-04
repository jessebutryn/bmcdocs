# UpdateCpld

Updates the motherboard CPLD of a managed system with the given CPLD firmware image. Use the `--index` option to specify the CPLD index for systems that support multiple motherboard CPLDs; without `--index`, the first motherboard CPLD is updated.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateCpld --file <filename> [--index <num>] --reboot
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateCpld --file <filename> [--index <num>] --reboot
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateCpld --file <filename> [--index <num>] --reboot
```

## Options

- `--file <file name>`: Updates the CPLD with the given CPLD image file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--individually`: (Optional) Updates each CPLD with corresponding configuration file individually.
- `--post_complete`: (Optional) Waits for the managed system's POST to complete after rebooting.
- `--index <number>`: (Optional) Updates the CPLD with the given index. The default value is empty, and the first CPLD will be updated.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateCpld --file CPLD.bin --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateCpld --file CPLD.bin --index 2 --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateCpld --file CPLD.bin --reboot
```

## Output

The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.

## Notes

- This command is only available on X13/H13 and later platforms and X12/H12 RoT systems.
- The system needs to be powered off while updating the CPLD firmware.
- This command will update the first motherboard CPLD by default without `--index` input.
