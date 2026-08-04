# SNMPManage

Manages Simple Network Management Protocol (SNMP) for the BMC. The action performed depends on the `--action` value.

## Actions

- `GetStatus`: Gets the BMC SNMP status
- `On`: Sets the SNMP server on
- `Off`: Sets the SNMP server off
- `GetCommunityString`: Gets the SNMP community string
- `SetCommunityString`: Sets the SNMP community string

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SNMPManage --action GetStatus
saa -i <IP or host name> -u <username> -p <password> -c SNMPManage --action On --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
saa -i <IP or host name> -u <username> -p <password> -c SNMPManage --action Off --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
saa -i <IP or host name> -u <username> -p <password> -c SNMPManage --action GetCommunityString
saa -i <IP or host name> -u <username> -p <password> -c SNMPManage --action SetCommunityString --community_string <community_string>
```

### In-Band
```
saa -c SNMPManage --action GetStatus
saa -c SNMPManage --action On --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
saa -c SNMPManage --action Off --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
saa -c SNMPManage --action GetCommunityString
saa -c SNMPManage --action SetCommunityString --community_string <community_string>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SNMPManage --action GetStatus
saa -l <system list file> [-u <username> -p <password>] -c SNMPManage --action On --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
saa -l <system list file> [-u <username> -p <password>] -c SNMPManage --action Off --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
saa -l <system list file> [-u <username> -p <password>] -c SNMPManage --action GetCommunityString
saa -l <system list file> [-u <username> -p <password>] -c SNMPManage --action SetCommunityString --community_string <community_string>
```

## Options

- `--action <action>`: Required. Sets action: `1` = GetStatus, `2` = On, `3` = Off, `4` = GetCommunityString, `5` = SetCommunityString
- `--snmp_id`: Assigns the SNMP index, in range [1-15]
- `--snmp_ip`: Sets the SNMP IP
- `--snmp_mac`: Sets the SNMP MAC address
- `--community_string`: Sets the SNMP community string

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SNMPManage --action GetStatus
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SNMPManage --action On --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SNMPManage --action Off --snmp_id <snmp id> --snmp_ip <snmp ip> --snmp_mac <snmp mac>
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD --c SNMPManage --action GetCommunityString
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SNMPManage --action SetCommunityString --community_string <community_string>
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SNMPManage --action GetStatus
[SAA_HOME]# ./saa -c SNMPManage --action On --snmp_id <snmp id> --snmp_ip <snmp ip> [--snmp_mac <snmp mac>]
[SAA_HOME]# ./saa -c SNMPManage --action Off --snmp_id <snmp id> --snmp_ip <snmp ip> --snmp_mac <snmp mac>
[SAA_HOME]# ./saa -c SNMPManage --action GetCommunityString
[SAA_HOME]# ./saa -c SNMPManage --action SetCommunityString --community_string <community_string>
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SNMPManage --action GetStatus
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SNMPManage --action On --snmp_id <snmp id> --snmp_ip <snmp ip> --snmp_mac <snmp mac>
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SNMPManage --action Off --snmp_id <snmp id> --snmp_ip <snmp ip> --snmp_mac <snmp mac>
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SNMPManage --action GetCommunityString
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SNMPManage --action SetCommunityString --community_string <community_string>
```

## Output

### --action GetStatus / On / Off
```
Done
Seq IP MAC Acknowledge
--- -- --- -----------
1 192.168.34.56 12:34:56:78:9A:BC on
2 0.0.0.0 00:00:00:00:00:00 off
3 0.0.0.0 00:00:00:00:00:00 off
4 0.0.0.0 00:00:00:00:00:00 off
5 0.0.0.0 00:00:00:00:00:00 off
6 0.0.0.0 00:00:00:00:00:00 off
7 0.0.0.0 00:00:00:00:00:00 off
8 0.0.0.0 00:00:00:00:00:00 off
9 0.0.0.0 00:00:00:00:00:00 off
10 0.0.0.0 00:00:00:00:00:00 off
11 0.0.0.0 00:00:00:00:00:00 off
12 0.0.0.0 00:00:00:00:00:00 off
13 0.0.0.0 00:00:00:00:00:00 off
14 0.0.0.0 00:00:00:00:00:00 off
15 0.0.0.0 00:00:00:00:00:00 off
```

## Notes

- The execution progress for the managed system is continuously updated to the "Execution Message" section of the managed system in the created log file.
