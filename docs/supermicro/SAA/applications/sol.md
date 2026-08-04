# SOL

Activates SOL (Serial-Over-LAN) or configures SOL parameters.

## Syntax

### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SOL --action <action> [[--bitrate <bitrate>] [--retryCount <retry count>] [--retryInterval <retryinterval>]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SOL --action <action> [[--bitrate <bitrate>] [--retryCount <retry count>] [--retryInterval <retryinterval>]]
```

## Actions

- **Activate**: Activates SOL.
- **Deactivate**: Stops SOL.
- **GetInfo**: Gets SOL information.
- **Set**: Sets SOL transmission bit rate, retry counts, and retry interval.

## Options

- `--action <action>`: Sets action to Activate, Deactivate, GetInfo, or Set.
- `--bitrate <bitrate>` (Optional): SOL transmission bit rate. Available SOL bit rates: `9.6|19.2|38.4|57.6|115.2` (kbps). Only supported with the Set action.
- `--retryCount <retry count>` (Optional): SOL retry counts. Only supported with the Set action.
- `--retryInterval <retry interval>` (Optional): The interval for BMC to retry sending SOL packets to the remote console. Set in milliseconds; the value should be ten or a multiple of ten. Only supported with the Set action.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SOL --action Activate

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SOL --action Set --bitrate 115.2
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SOL --action Set --retryCount 3
```

## Notes

- With the Activate action, SOL turns on in the current text mode; press `<F12>` to exit. Displaying the remote text console requires the computer terminal or terminal emulator running SAA to support ANSI/VT100 terminal control escape sequences.
- Command SOL does not support local in-band usage.
- The Activate action does not support multiple system usage.
