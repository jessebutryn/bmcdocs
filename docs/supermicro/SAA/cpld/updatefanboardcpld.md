# UpdateFanboardCpld

Updates the Fanboard CPLD of a managed system with the given Fanboard CPLD firmware image. Runs on CPLD RoT systems of X13/H13 and later platforms.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateFanboardCpld --file <filename> --type <Fanboard_ID> [--index <CPLD_ID>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateFanboardCpld --file <filename> --type <Fanboard_ID> [--index <CPLD_ID>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateFanboardCpld --file <filename> --type <Fanboard_ID> [--index <CPLD_ID>]
```

## Options

- `--file <file name>`: Updates the Fanboard CPLD with the given Fanboard CPLD image file.
- `--type`: Sets action to: 1 = Front, 2 = Rear, or the corresponding Fanboard ID number.
- `--index <number>`: (Optional) Sets the CPLD index. The default value is 1, and the index count starts from 1.
- `--individually`: (Optional) Updates each Fanboard CPLD with the corresponding configuration file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateFanboardCpld --file Fanboard_CPLD.bin --type Front
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateFanboardCpld --file Fanboard_CPLD.bin --type Rear --index 1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateFanboardCpld --file Fanboard_CPLD.bin --type Front
```

## Output

The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
