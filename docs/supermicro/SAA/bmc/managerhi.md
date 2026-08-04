# ManageRHI

Switches the Redfish Host Interface USB connection to CDC-ECM or RNDIS mode.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ManageRHI --action <GetConnection | SetConnection> [--type <RNDIS | CDC_ECM>]
```

### In-Band
```
saa -c ManageRHI --action <GetConnection | SetConnection> [--type <RNDIS | CDC_ECM>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ManageRHI --action <GetConnection | SetConnection> [--type <RNDIS | CDC_ECM>]
```

## Options

- `--action <action>`: Required. Sets action: `1` = GetConnection, `2` = SetConnection
- `--type <type>`: Sets USB connection type: `0` = RNDIS, `1` = CDC_ECM (the input type string is converted to the corresponding type number)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ManageRHI --action GetConnection
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ManageRHI --action SetConnection
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ManageRHI --action GetConnection
[SAA_HOME]# ./saa -c ManageRHI --action SetConnection --type CDC_ECM
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ManageRHI --action GetConnection
```
