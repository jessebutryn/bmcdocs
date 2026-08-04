# GetSasExpanderInfo

Gets the SAS Expander firmware image and its corresponding information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSasExpanderInfo [--file <filename>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetSasExpanderInfo [--file <filename>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSasExpanderInfo [--file <filename>]
```

## Options

- `-I Redfish_HI`: Uses the Redfish Host Interface to query the firmware information. Only in-band usage is supported (optional).
- `--file <file name>`: Reads the SAS Expander information from an input image file (optional).
- `--file_only`: Works with the `--file` option, and only reads SAS Expander information from the input image file (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSasExpanderInfo --file BPN_SAS3.rom
```

### In-Band (Redfish Host Interface)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetSasExpanderInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSasExpanderInfo
```

## Output

```
Managed system...............................192.168.34.56
 [SAS Expander 1]
 SAS Expander Name....................SASExpander Device 0
 SAS Expander Version.................99.25.01.02
Local SAS Expander image file................BPN_SAS3.rom
 SAS Expander Name........................826SE1
 SAS Expander Version.....................00.25.00.01
```

## Notes

- The execution progress for the managed system will be continuously updated to the Execution Message section of the created log file.
