# ChangeTpInfo

Updates the TwinPro configuration of the managed system with the given, previously edited configuration file (e.g. TpInfo.xml).

To use this command:

1. Select one managed system as the golden sample for current BMC settings (for multiple-systems usage).
2. Use `GetTpInfo` to retrieve the current TwinPro settings.
3. Edit the configurable element values in the BMC configuration text file (e.g. TpInfo.xml) to the desired values.
4. Optionally skip unchanged tables in the text file by setting the `Action` attribute to `None`.
5. Optionally remove unchanged tables/elements from the text file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeTpInfo --file <filename>
```

### In-Band
```
saa -c ChangeTpInfo --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeTpInfo --file <filename> [--individually]
```

## Options

- `--file <file name>`: Updates the TwinPro configuration with the given configuration file.
- `--individually`: (Optional) Updates each set of TwinPro configurations with the corresponding configuration file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeTpInfo --file TpInfo.xml
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeTpInfo --file TpInfo.xml
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeTpInfo --file TpInfo.xml

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeTpInfo --file TpInfo.xml --individually
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
- To update multiple systems (e.g., 192.168.34.56 and 192.168.34.57), you need to provide two files, `TpInfo.xml.192.168.34.56` and `TpInfo.xml.192.168.34.57`, and set the `--file` argument to the base `TpInfo.xml` file name. With the `--individually` option, SAA will search for `TpInfo.xml.192.168.34.56` and `TpInfo.xml.192.168.34.57` to update each system respectively.
