# ChassisIntrusion

Gets and clears the status of the chassis intrusion sensor on the managed system.

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c ChassisIntrusion --action <action>
```

## Actions

- **Status**: Get the current chassis intrusion status
- **Clear**: Clear/reset the chassis intrusion status

## Examples

### OOB - Get Status
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChassisIntrusion --action Status
```

### In-Band - Clear Status
```bash
[SUM_HOME]# sudo ./sum -c ChassisIntrusion --action Clear
```

## Output

### Status Action
```
Managed system................localhost
 Intrusion Sensor..........Normal
```

### Clear Action
```
Chassis intrusion has already been cleared.
```

## Notes

- Status shows "Hardware Intrusion" if intrusion detected, otherwise "Normal"
- In-band clear action requires sudo privileges
- Supported for both OOB and in-band usage
