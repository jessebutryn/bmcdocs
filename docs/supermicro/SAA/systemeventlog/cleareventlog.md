# ClearEventLog

Clears the event log (both BMC and BIOS event logs) on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ClearEventLog [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]] [--clear_bmc_eventlog] [--clear_bios_eventlog]
```

### In-Band
```
saa -c ClearEventLog [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot] [--clear_bmc_eventlog] [--clear_bios_eventlog]
```

### Multiple Systems OOB
```
saa -l <system list file> -u [<username> -p <password>] -c ClearEventLog [--current_password <current password> | --cur_pw_file <current password file path>] [--reboot [--post_complete]] [--clear_bmc_eventlog] [--clear_bios_eventlog]
```

## Options

- `--current_password <current password>`: Checks the current BIOS Administrator password
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password
- `--reboot`: Forces the managed system to reboot or power up after operation
- `--post_complete`: Waits for the managed system's POST to complete after reboot
- `--clear_bmc_eventlog`: Only clears the BMC event log
- `--clear_bios_eventlog`: Only clears the BIOS event log

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ClearEventLog --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ClearEventLog --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ClearEventLog --reboot
```

## Notes

- If the execution "Status" field for a managed system is SUCCESS, its event logs are cleared.
