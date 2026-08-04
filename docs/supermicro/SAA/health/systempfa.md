# SystemPFA

Monitors and sets the Predictive Failure Analysis (PFA) function of BIOS on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SystemPFA {--action <action>} [--reboot [--post_complete]]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c SystemPFA {--action <action>} [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SystemPFA {--action <action>} [--reboot [--post_complete]]
```

## Options

- `--action <action>`: Sets action:
    - `1` = GetCurrentStatus
    - `2` = Enabled
    - `3` = Disabled
- `--reboot`: (Optional) Forces the managed system to reboot or power up after the operation.
- `--post_complete`: (Optional) Waits for the managed system's POST to complete after rebooting.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SystemPFA --action GetCurrentStatus

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SystemPFA --action Enabled --reboot --post_complete
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SystemPFA --action Disabled --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SystemPFA --action Enable --reboot --post_complete
```

If the execution "Status" field for a managed system is SUCCESS, the utilization status of the managed system is shown in the "Execution Message" section in the created log file.

## Output

### GetCurrentStatus
```
The current system PFA is Disabled
```

### Enabled/Disabled with reboot
```
The system PFA is set to Enabled.
Status: The managed system 192.168.34.56 is rebooting.
..........................Done
Status: The managed system 192.168.34.56 is waiting for POST complete
........................
..................................................
..................................................
..................................................
......
Status: The managed system 192.168.34.56 is POST completed
```
