# GetSmartData

Gets NVMe S.M.A.R.T. data information for a specified device.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSmartData --device_name <DEVICE_NAME>
```

### In-Band
```
saa -c GetSmartData --device_name <DEVICE_NAME>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSmartData
```

## Options

- `--device_name <HDD Name>`: Gets the specified device's smart data (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSmartData --device_name vmhba1
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetSmartData --device_name vmhba1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSmartData
```

## Output

```
[Device name : vmhba1]
 Critical warning : 0
 IB Temp. : 324 K
 Available spare : 99 %
 Available spare threshold : 10 %
 Percentage used : 0 %
 Data units read (512k bytes) : 0x84c55b
 Data units written (512k bytes) : 0x1734d9
 Host read commands : 0x6ed1332
 Host write commands : 0x1234ee2
 Controller busy time (minutes) : 0x8
 Power cycles : 0x38e8
 Power on hours : 0x2df3
 Unsafe shutdowns : 0x2a20
 Media errors : 0x0
 Error log entries : 0x0
```

## Notes

- If the execution Status field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
