# UpdateNICCpld

Updates the NIC CPLD firmware on the managed system with the given CPLD image file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateNICCpld --file <filename> [--dev_id <Device ID>]
```

### In-Band
```
saa -I Redfish_HI -c UpdateNICCpld --file <filename> [--dev_id <Device ID>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateNICCpld --file <filename> [--dev_id <Device ID>] [--individually]
```

## Options

- `--file <file name>`: Updates the NIC CPLD with the given CPLD image file.
- `--individually`: (Optional) Updates each CPLD on NIC with its corresponding image file individually.
- `--dev_id <Device ID>`: (Optional) Updates the CPLD on NIC with the given NIC ID and CPLD ID. The CPLD for the first NIC is updated by default. e.g., NIC 1 and CPLD 1: `--dev_id 1_1`

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateNICCpld --file NIC_CPLD.jed
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateNICCpld --file NIC_CPLD.jed --dev_id 1_1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateNICCpld --file NIC_CPLD.jed
```
