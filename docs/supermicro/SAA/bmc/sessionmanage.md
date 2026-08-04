# SessionManage

Manages BMC Redfish sessions.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SessionManage --action [GetInfo | Disconnect --session_id <session_id>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c SessionManage --action [GetInfo | Disconnect --session_id <session_id>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SessionManage --action [GetInfo | Disconnect --session_id <session_id>]
```

## Options

- `--action <action>`: Required. `GetInfo` to get Redfish session information, or `Disconnect` (with `--session_id`) to disconnect a session
- `--session_id <session_id>`: The session ID to disconnect (used with `--action Disconnect`)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SessionManage --action GetInfo
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SessionManage --action Disconnect --session_id 1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SessionManage --action GetInfo
```

## Output

### --action GetInfo
```
Managed system............................192.168.34.56
 Session service enabled...............True
 Session timeout.......................1800
 Number of currently active sessions...2
 Session ID............................1
 User Name.........................ADMIN
 Session ID............................2
 User Name.........................USER
```

### --action Disconnect
```
Session 1 is disconnected.
```
