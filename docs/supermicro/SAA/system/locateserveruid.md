# LocateServerUid

Controls the UID (unit identifier) of the managed system, used for easy system location in large stack configurations. When the UID is enabled, the blue LED on both the front and rear of the chassis is illuminated.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c LocateServerUid --action <action>
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c LocateServerUid --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c LocateServerUid --action <action>
```

## Options

- `--action <action>`: Sets action:
    - `1` = GetStatus
    - `2` = On
    - `3` = Off

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c LocateServerUid --action 3
```

### In-Band
```bash
[SAA_HOME]# ./saa -c LocateServerUid --action GetStatus
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c LocateServerUid --action 3
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system is shown in the "Execution Message" section of the created log file.

## Output

### Off
```
UID of the managed system is turned off.
Managed system................localhost
 UID status................Off
```
