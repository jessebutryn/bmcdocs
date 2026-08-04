# GetMultinodeLcmcInfo

Gets the multi-node LCMC firmware image information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetMultinodeLcmcInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetMultinodeLcmcInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetMultinodeLcmcInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMultinodeLcmcInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetMultinodeLcmcInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMultinodeLcmcInfo
```

## Output

```
Managed system.....................169.254.3.254
 LCMC version...................0.07
```

## Notes

- The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
