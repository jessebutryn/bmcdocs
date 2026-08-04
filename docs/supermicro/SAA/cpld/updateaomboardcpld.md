# UpdateAomboardCpld

Updates the AOM board CPLD on the managed system with the given AOM board CPLD firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateAomboardCpld --file <filename> [--dev_id <id>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateAomboardCpld --file <filename> [--dev_id <id>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateAomboardCpld --file <filename> [--dev_id <id>]
```

## Options

- `--file <file name>`: Updates the AOM board CPLD with the given CPLD image file.
- `--individually`: (Optional) Updates each AOM board CPLD with its corresponding image file individually.
- `--dev_id <Device ID>`: (Optional) Updates the AOM board CPLD with the given AOM device ID. The default value is empty, and the CPLD for the first AOM board will be updated.
- `--index <number>`: (Optional) Updates the CPLD with the given index. The default value is empty, and the first CPLD on the AOM board will be updated.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateAomboardCpld --file AOM_CPLD.jed --dev_id 1
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateAomboardCpld --file AOM_CPLD.jed
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateAomboardCpld --file AOM_CPLD.jed
```

## Output

The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
