# GetAiomStandbyPower

Retrieves AIOM Standby Power configuration information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetAiomStandbyPower
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetAiomStandbyPower
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetAiomStandbyPower
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetAiomStandbyPower
```

### In-Band (Redfish Host Interface)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetAiomStandbyPower
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetAiomStandbyPower
```

## Output

```
Managed system............................................................192.168.34.56
AIOM NIC Power in S5 State (Shutdown) ....................................On
```
