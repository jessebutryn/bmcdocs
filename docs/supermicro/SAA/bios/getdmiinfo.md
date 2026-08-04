# GetDmiInfo

Gets the current supported editable DMI (Desktop Management Interface) information from the managed system and saves it in a DMI.txt file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetDmiInfo [--file <DMI.txt> [--overwrite]]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetDmiInfo [--file <DMI.txt> [--overwrite]]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c GetDmiInfo [--file <DMI.txt> [--overwrite]] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetDmiInfo [--file <DMI.txt> [--overwrite]]
```

## Options

- `--file <file name>`: Saves the DMI information to a file (prints on screen if the file-saving function is not available)
- `--overwrite`: Overwrites the output file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetDmiInfo --file DMI.txt --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetDmiInfo --file DMI.txt --overwrite
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetDmiInfo --file DMI.txt --overwrite --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetDmiInfo --file DMI.txt --overwrite
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetDmiInfo --file DMI.txt --overwrite
```

## Notes

- This DMI file is synchronized to the BMC from the BIOS when the system reboots or powers up.
- If the BMC firmware image has been reflashed, this function will not work until the managed system is first rebooted or powered up.
- The supported editable DMI items can vary from BIOS to BIOS; SAA only shows supported items.
- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its DMI settings are saved in its output file, e.g., `DMI.txt.192.168.34.56`. The `--overwrite` option forces overwrite of an existing file.
