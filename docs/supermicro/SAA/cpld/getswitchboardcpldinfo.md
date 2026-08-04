# GetSwitchboardCpldInfo

Gets the firmware information for all switchboard CPLDs (Main, Left, Right) installed on the managed system. Supported on CPLD RoT systems of X13/H13 and later platforms. Currently only supported through Redfish communication, so in-band usage can only be done through the Redfish Host Interface.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSwitchboardCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetSwitchboardCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSwitchboardCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSwitchboardCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSwitchboardCpldInfo
```

## Output

The console output contains information for all switchboard CPLDs that can be updated:

```
Managed system.....................192.168.34.56
 [Main Switchboard]
 CPLD 1 version.............10
 CPLD 2 version.............0F
 [Left Switchboard]
 CPLD 2 version.............32
 [Right Switchboard]
 CPLD 2 version.............3F
```

### Switchboard CPLD Types

| Type | Description |
|------|-------------|
| Main Switchboard | It is possible to install many main switchboards. |
| Left Switchboard | It is possible to install many left switchboards. Left switchboard can only be displayed if the system has fully booted up. |
| Right Switchboard | It is possible to install many right switchboards. Right switchboard can only be displayed if the system has fully booted up. |

## Notes

- DO NOT update CPLD firmware with a wrong index.
- If the execution "Status" field for the managed system is SUCCESS, the information will be shown in the "Execution Message" section of the managed system in the created log file.
- Left/Right Switchboard CPLD #1 is not supported for the user to get information about.
- Limitation: when the system is in the process of powering up, this command can fail. Wait for the system to fully boot up and try again.
