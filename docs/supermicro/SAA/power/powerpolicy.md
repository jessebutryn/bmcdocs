# PowerPolicy

Manages power policy through Intel Intelligent Power Node Manager (`--type NM20`) or BMC Intel Node Manager (`--type BMC10`) for Supermicro Intel platforms. Supports enabling/disabling policy control globally, per domain, and per policy; adding, getting, deleting, and scanning policies; managing alert thresholds; and (NM20 only) managing suspension periods.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c PowerPolicy --type <NM20|BMC10> --action <action> [options...]
```

### In-Band
```
saa -c PowerPolicy --type <NM20|BMC10> --action <action> [options...]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c PowerPolicy --type <NM20|BMC10> --action <action> [options...]
```

## Actions

Actions supported by both `--type NM20` (Intel Intelligent Power Node Manager 2.0) and `--type BMC10` (BMC Intel Node Manager 1.0):

- **EnableGlobal**: Enables NM policy control globally.
- **DisableGlobal**: Disables NM policy control globally.
- **EnableDomain**: Enables NM policies for the specified domain.
- **DisableDomain**: Disables NM policies for the specified domain.
- **EnablePolicy**: Enables the specified NM policy.
- **DisablePolicy**: Disables the specified NM policy.
- **AddPowerPolicy**: Adds a power policy using simplified defaults for mode/domain/trigger.
- **AddPolicy**: Adds a policy with full control over mode, domain, and trigger options.
- **GetPolicy**: Gets a policy.
- **DelPolicy**: Deletes a policy.
- **ScanPolicy**: Scans all presented policies.

Additional actions supported only by `--type NM20`:

- **GetAlertThreshold**: Gets policy alert thresholds.
- **SetAlertThreshold**: Sets policy alert thresholds.
- **GetPeriod**: Displays the suspension period.
- **AddPeriod**: Adds a suspension period.
- **UpdatePeriod**: Updates a suspension period.
- **DeletePeriod**: Deletes a suspension period.
- **ClearPeriod**: Clears the suspension period.

Additional actions supported only by `--type BMC10`:

- **GetLimitPolicyId**: Gets the limiting policy ID.
- **GetPsysInfo**: Gets Platform Power (Psys) information.

## Options

- `--type <type>`: `NM20` (Node Manager 2.0) or `BMC10` (BMC Intel Node Manager 1.0).
- `--action <action>`: The action to perform (see Actions above).
- `--domain_id <Domain ID>`: Domain to target.
  - For `NM20`: `0` = Entire platform, `1` = CPU subsystem, `2` = Memory subsystem, `4` = High Power I/O subsystem.
  - For `BMC10`: `0` = Entire platform, AC power (Psys support required), `1` = CPU subsystem, `2` = Memory subsystem, `4` = PCIe devices subsystem (Psys support required), `5` = Entire platform, DC power (Psys support required).
- `--policy_id <Policy ID>`: Specifies policy ID from 0 to 255.
- `--limit <Limit>`: Policy target limit (watts). For `AddPolicy` with `BMC10`, the valid range depends on `--trigger_type` (0-32767 watts, or 0-100 percentage for trigger type 2; not required for trigger type 9).
- `--mode <Mode>`: Aggressive CPU power correction mode. `0` = Automatic, `1` = Force non-aggressive, `2` = Force aggressive. Defaults to Automatic if omitted.
- `--period <Period>`: Statistics reporting period in seconds (NM20: no explicit range documented; BMC10: 1-3600).
- `--exception_action <Exception action>`: Policy exception action. `1` = Send alert, `2` = Shutdown system, `3` = Send alert & shutdown system (NM10/NM20 AddPolicy). `BMC10 SetAlertThreshold`/`DcmiManage` style values differ per context.
- `--time <Time>`: Correction time limit in milliseconds (BMC10: 1000-60000).
- `--trigger_type <Trigger Type>`: Policy trigger type.
  - `NM20`: `0` = No policy trigger, `1` = Inlet temperature limit (Celsius), `2` = Missing power reading timeout (1/10th second), `3` = Time after host reset trigger (1/10th second), `4` = Boot time policy, `6` = MGPIO policy trigger.
  - `BMC10`: `0` = No policy trigger, `1` = Inlet temperature limit (Celsius), `2` = Missing power reading timeout (1/10th second), `3` = Time after host reset trigger (1/10th second), `6` = MGPIO policy trigger, `7` = C0 Residency (%), `8` = Host Reset, `9` = SMBAlert Interrupt.
- `--trigger_limit <Trigger Limit>`: Policy trigger limit; meaning depends on `--trigger_type`. Defaults to the policy target limit if omitted.
- `--storage <Storage>`: (BMC10 `AddPolicy`/`AddPowerPolicy` only) `0` = Persistent storage, `1` = Volatile memory.
- `--overwrite`: Overwrites the policy (optional).
- `--value <Value>`: Threshold value(s) for `SetAlertThreshold` — up to three values separated by commas (optional).
- `--count <Count>`: For `SetAlertThreshold`: `0` clears all thresholds, `[1-3]` sets the number of alert thresholds.
- `--period_id <Period ID>`: Period ID 1-5, used by `UpdatePeriod`, `DeletePeriod`, and `ClearPeriod` (NM20 only).
- `--st <Start time>`: Policy suspension start time, format HHmm `[0000-2359]` (optional).
- `--et <End time>`: Policy suspension end time, format HHmm `[0006-2400]` (optional).
- `--days <Day>`: Suspend period recurrence: `1` = Monday ... `7` = Sunday (optional).

## Examples

### Enable/Disable Global Policy Control (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action EnableGlobal
[SAA_HOME]# ./saa -c PowerPolicy --type NM20 --action DisableGlobal
```

### Enable/Disable Domain (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action EnableDomain --domain_id 0
[SAA_HOME]# ./saa -c PowerPolicy --type NM20 --action DisableDomain --domain_id 0
```

### Enable/Disable Specific Policy (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action EnablePolicy --domain_id 0 --policy_id 1
[SAA_HOME]# ./saa -c PowerPolicy --type NM20 --action DisablePolicy --domain_id 0 --policy_id 1
```

### Adding a Power Policy (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action AddPowerPolicy --policy_id 1 --limit 200 --time 20000 --period 200 --overwrite

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action AddPolicy --domain_id 0 --policy_id 1 --trigger_type 0 --mode 0 --exception_action 1 --limit 200 --time 20000 --trigger_limit 200 --period 200 --overwrite
```

### Adding a Power Policy (BMC10)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type BMC10 --action AddPowerPolicy --domain_id 0 --policy_id 1 --limit 200 --time 20000 --period 200 --storage 1 --overwrite

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type BMC10 --action AddPolicy --domain_id 0 --policy_id 1 --trigger_type 0 --mode 0 --exception_action 1 --limit 200 --time 20000 --trigger_limit 200 --period 200 --storage 1 --overwrite
```

### Getting/Deleting/Scanning Policy
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action GetPolicy --domain_id 0 --policy_id 1
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action DelPolicy --domain_id 0 --policy_id 1
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action ScanPolicy
```

### Alert Thresholds (NM20 only)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action GetAlertThreshold --domain_id 0 --policy_id 1

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action SetAlertThreshold --domain_id 0 --policy_id 1 --count 3 --value 100,200,300
```

### Suspension Periods (NM20 only)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action GetPeriod --domain_id 0 --policy_id 0

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action AddPeriod --domain_id 0 --policy_id 0 --st 0000 --et 0006 --days 123

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action UpdatePeriod --domain_id 0 --policy_id 0 --period_id 1 --st 0000 --et 0006 --days 123

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action DeletePeriod --domain_id 0 --policy_id 0 --period_id 1

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action ClearPeriod --domain_id 0 --policy_id 0 --period_id 1
```

### GetLimitPolicyId / GetPsysInfo (BMC10 only)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type BMC10 --action GetLimitPolicyId

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c PowerPolicy --type BMC10 --action GetPsysInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c PowerPolicy --type NM20 --action EnableGlobal
```

## Output

### ScanPolicy (NM20)
```
=============================================
Domain ID = 0 , Policy ID = 3
=============================================
Values:
Power Limit = 200 w
Correction Time limit = 20000 ms
Statistics Reporting Period = 200 s
Policy Trigger Limit = 200
Domain ID:
 Entire platform
Policy state:
 Policy(Enabled) Domain(Enabled) Global(Enabled)
Policy Trigger Type:
 No Policy Trigger
Aggressive CPU Power correction:
 Backward compatible with NMV1.5
Policy Exception action state:
 Send alert
raw = 57 01 00 70 10 01 C8 00 20 4E 00 00 C8 00 C8 00
Alert Thresholds:
Number of alert thresholds = 0
Suspend Periods:
Number Of Periods = 0
Total Policies = 1
```

### GetAlertThreshold
```
Number of alert thresholds = 3
Threshold[0] = 150
Threshold[1] = 250
Threshold[2] = 300
```

### GetPeriod
```
Number Of Periods = 1
[Suspend Periods 1]
 Start = 00:00
 Stop = 23:54
 Days = Monday Tuesday Wednesday
```

### GetPolicy (BMC10)
```
Values:
Power Limit = 210 w
Correction Time limit = 6000 ms
Statistics Reporting Period = 10 s
Policy Trigger Limit = 210
Domain ID:
 CPU subsystem
Policy state:
 Policy(Enabled) Domain(Enabled) Global(Disabled)
Policy Trigger Type:
 No Policy Trigger
Aggressive CPU Power correction:
 Backward compatible with NMV1.5
Policy Exception action state:
 Send alert
raw = 57 01 00 31 90 01 D2 00 70 17 00 00 D2 00 0A 00
```

### GetLimitPolicyId
```
Current limiting policy ID = 1
```

### GetPsysInfo
```
Psys support..............Yes
```

## Notes

- Starting from X14 and later platforms, use `--type BMC10` instead of `NM20` — these platforms lack a Management Engine (ME) and cannot support Intel Node Manager management.
- When managing power policy through BMC Intel Node Manager (`--type BMC10`), some domain management requires Platform Power (Psys) support. The `--domain_id` values `0` (Entire platform, AC power), `4` (PCIe devices subsystem), and `5` (Entire platform, DC power) require Psys support.
- The `--period` option (Statistic Reporting Period) specifies the period for calculating average power when the Node Manager reports performance statistics.
- The execution progress for the managed system is continuously updated in the Execution Message section of the created log file.
