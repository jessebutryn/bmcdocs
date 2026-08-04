# ChassisIntrusion

Gets and clears the status of the chassis intrusion sensor. If a hardware intrusion is detected, the status is "Hardware Intrusion"; otherwise it is "Normal". This command can either get the status or set the status to "Normal".

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChassisIntrusion --action {Clear | Status}
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c ChassisIntrusion --action {Clear | Status}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChassisIntrusion --action {Clear | Status}
```

## Options

- `--action <action>`: Sets action:
    - `1` = Status
    - `2` = Clear

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChassisIntrusion --action Status
```

### In-Band
```bash
[SAA_HOME]# sudo ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChassisIntrusion --action Clear
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChassisIntrusion --action Status
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the chassis intrusion information of the managed system is shown in the "Execution Message" section in the created log file.

## Output

### Status
```
Managed system................localhost
Intrusion Sensor..........Normal
```

### Clear
```
Chassis intrusion has already been cleared.
```
