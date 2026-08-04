# GetMidplaneSbbCpldInfo

Gets the Midplane Storage Bridge Bay (SBB) CPLD information from the managed system installed directly on the NVMe backplane.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetMidplaneSbbCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetMidplaneSbbCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetMidplaneSbbCpldInfo
```

## Options

- `-I Redfish_HI`: (Optional) Uses Redfish Host Interface to query the firmware information. (Only in-band usage is supported.)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMidplaneSbbCpldInfo
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c GetMidplaneSbbCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMidplaneSbbCpldInfo
```

## Output

```
Managed system.........................192.168.34.56
 Midplane SBB CPLD 1 version........CPLD_ID: 0000 REV: 01
```

```
Managed system.........................169.254.3.254
 Midplane SBB CPLD 1 version........CPLD_ID: 0000 REV: 01
```

## Notes

- This command is supported on systems with Midplane board type.
- If the "Status" field of the managed system shows SUCCESS, the console output will be displayed in the "Execution Message" section of the managed system in the created log file.
