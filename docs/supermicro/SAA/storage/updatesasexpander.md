# UpdateSasExpander

Updates the SAS Expander firmware of a managed system with the given SAS Expander firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateSasExpander --file <filename> --index 1 [--reboot]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateSasExpander --file <filename> --index 1 [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateSasExpander --file <filename> --index 1 [--reboot]
```

## Options

- `--file <file name>`: Updates SAS Expander with the given image file.
- `--index <index>`: Sets the SAS Expander index that needs to be updated.
- `--reboot`: Forces the managed system to reboot or power up after operation (optional).
- `-I Redfish_HI`: Uses the Redfish Host Interface to query the firmware information. Only in-band usage is supported (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateSasExpander --file SAS_FW.rom --index 1 --reboot
```

### In-Band (Redfish Host Interface)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateSasExpander --file SAS_FW.rom --index 1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateSasExpander --file SAS_FW.rom --index 1
```

## Output

```
Managed system............................169.254.3.254
 [SAS Expander 1]
 SAS Expander Name....................SASExpander Device 0
 SAS Expander Version.................00.25.00.01
```

## Notes

- The execution progress for the managed system will be continuously updated in the Execution Message section of the created log file.
