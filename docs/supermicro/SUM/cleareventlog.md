# ClearEventLog

Clears the system event log (both BMC and BIOS event logs) on the managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c ClearEventLog [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--reboot] [--clear_bmc_eventlog] [--clear_bios_eventlog]
```

## Options

- `--current_password <current password>`: Current BIOS password (if set)
- `--cur_pw_file <current password file path>`: File containing current BIOS password
- `--reboot`: Reboot system after clearing logs
- `--clear_bmc_eventlog`: Clear only BMC event logs
- `--clear_bios_eventlog`: Clear only BIOS event logs

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ClearEventLog --reboot
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ClearEventLog --reboot
```

## Notes

- BMC event logs are cleared immediately
- BIOS event logs are cleared only after system reboot
- If no specific log type is specified, both BMC and BIOS logs are cleared
