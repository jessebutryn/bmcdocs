# HDTService

Gets or sets the hardware debug tool (HDT) status of the BMC system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c HDTService --action <action>
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c HDTService --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c HDTService --action <action>
```

## Options

- `--action <action>`: Sets action:
    - `1` = GetHDTStatus
    - `2` = Enable
    - `3` = Disable

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c HDTService --action GetHDTStatus
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c HDTService --action Enable
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c HDTService --action Disable
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the "Status" field in the execution of the managed system displays SUCCESS, the console output of the managed system appears in the "Execution Message" section of the created log file.

## Output

### GetHDTStatus
```
HDT is disabled.
```

### Enable
```
The HDT is set to Enable.
```
