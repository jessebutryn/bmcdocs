# SetAiomStandbyPower

Configures the AIOM Standby Power settings for the managed system, controlling the AIOM network card and standby fan(s). Default setting is On.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetAiomStandbyPower --action <action>
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c SetAiomStandbyPower --action <action>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetAiomStandbyPower --action <action>
```

## Options

- `--action <action>`: Sets action to `1` = On, `2` = Off.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetAiomStandbyPower --action On
```

### In-Band (Redfish Host Interface)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SetAiomStandbyPower --action Off
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetAiomStandbyPower --action Off
```

## Output

### Power On
```
Proceeding to AIOM Standby Power On the managed system.
Managed system............................................................192.168.34.56
AIOM NIC Power in S5 State (Shutdown) ....................................On
```

### Power Off
```
Proceeding to AIOM Standby Power Off the managed system.
Managed system............................................................192.168.34.56
AIOM NIC Power in S5 State (Shutdown) ....................................Off
```
