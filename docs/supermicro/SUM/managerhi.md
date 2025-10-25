# ManageRHI

Manages Redfish Host Interface USB connection mode.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c ManageRHI --action <GetConnection | SetConnection> [--type <RNDIS | CDC_ECM>]
```

## Options

- `--action <GetConnection | SetConnection>`: Action to perform.
  - `GetConnection`: Get current USB connection mode.
  - `SetConnection`: Set USB connection mode.
- `--type <RNDIS | CDC_ECM>`: USB connection type (required for SetConnection action).

## Examples

### OOB Get Connection
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ManageRHI --action GetConnection
```

### OOB Set Connection to RNDIS
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ManageRHI --action SetConnection --type RNDIS
```

### In-Band Get Connection
```
[SUM_HOME]# ./sum -c ManageRHI --action GetConnection
```

### In-Band Set Connection to CDC_ECM
```
[SUM_HOME]# ./sum -c ManageRHI --action SetConnection --type CDC_ECM
```

## Notes

- This command switches the USB connection to CDC-ECM or RNDIS mode for Redfish Host Interface.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/managerhi.md