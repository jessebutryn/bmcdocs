# GetPMemInfo

Gets the PMem firmware image information from the managed system, as well as information from a local PMem firmware image (with the `--file` option).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetPMemInfo [--file <filename>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetPMemInfo [--file <filename>]
saa -c GetPMemInfo --file <filename> --file_only
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetPMemInfo [--file <filename>]
```

## Options

- `--file <file name>`: Reads the PMem information from an input PMem image file (optional).
- `--file_only`: Works with the `--file` option, and only reads PMem information from the input image file (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPMemInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetPMemInfo --file PMem.bin

[SAA_HOME]# ./saa -c GetPMemInfo --file PMem.bin --file_only
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetPMemInfo --file PMem.bin
```

## Output

```
Managed system................192.168.34.56
 PMem version..............2.2.0.1464
Managed system................169.254.3.254
 PMem version..............2.2.0.1464
Local PMem image file.........PMem.bin
 PMem version..............2.2.0.1469
```

## Notes

- This command is available on X12 3rd Gen Intel Xeon Scalable processors with Intel C621A Series Chipsets and later platforms.
- The PMem firmware version retrieved from `GetPMemInfo` is the running PMem firmware version.
- For more detailed usage of PMem, contact Supermicro technical support.
- If the execution Status field for a managed system is SUCCESS, the PMem information of the managed system will be shown in the Execution Message section of the created log file.
