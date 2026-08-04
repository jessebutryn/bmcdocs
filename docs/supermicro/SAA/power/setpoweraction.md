# SetPowerAction

Sets the type of power action for the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetPowerAction --action <action> [--interval <time interval>] [--post_complete]
```

### In-Band
```
saa -c SetPowerAction --action <action> [--interval <time interval>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetPowerAction --action <action> [--interval <time interval>] [--post_complete]
```

## Options

- `--action <action>`: Sets power action to:
  - `0` = up
  - `1` = down
  - `2` = cycle
  - `3` = reset
  - `4` = softshutdown
  - `5` = reboot
  - `6` = accycle
  - `7` = nmi
  - `8` = on
- `--interval <time interval>`: Sets the power cycle interval in seconds (optional).
- `--post_complete`: Waits for the managed system's POST to complete after reboot (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetPowerAction --action up
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetPowerAction --action 0
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SetPowerAction --action up
[SAA_HOME]# ./saa -c SetPowerAction --action 0
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetPowerAction --action up
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetPowerAction --action 0
```

## Output

```
Proceeding to power up the managed system.
```

## Notes

- `up` maps to the Redfish `ForceOn` reset type, and `on` maps to Redfish `On`.
- The supported `--action` values are extracted from the Redfish `ResetActionInfo` response, and may vary by platform. For example, query supported actions with:
  ```
  curl -k -X GET -H "Content-Type: application/json" -u "ADMIN:ADMIN" "https://<BMC_IP>/redfish/v1/Systems/System_0/ResetActionInfo"
  ```
- If the execution Status field for a managed system is SUCCESS, the BIOS and BMC capabilities of the managed system will be shown in the Execution Message section of the created log file.
