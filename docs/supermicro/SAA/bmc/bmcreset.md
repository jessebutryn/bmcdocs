# BmcReset

Sets the BMC to cold reset or warm reset for the target system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BmcReset --action <ColdReset | WarmReset> [--bmc_boot_check]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c BmcReset --action <ColdReset | WarmReset>
saa -c BmcReset --action <ColdReset | WarmReset> [--bmc_boot_check]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c BmcReset --action <ColdReset | WarmReset> [--bmc_boot_check] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BmcReset --action <ColdReset | WarmReset> [--bmc_boot_check]
```

## Options

- `--action <action>`: Required. Sets action to `1` = ColdReset, `2` = WarmReset
- `--bmc_boot_check`: Checks BMC boots up within 4 minutes after reset

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcReset --action ColdReset
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcReset --action WarmReset --bmc_boot_check
```

### In-Band
```bash
[SAA_HOME]# ./saa -c BmcReset --action ColdReset
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c BmcReset --action ColdReset
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c BmcReset --action WarmReset --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c BmcReset --action WarmReset --bmc_boot_check --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l IP_ADDR_RANGE.txt -u ADMIN -p ADMIN -c BmcReset --bmc_boot_check --action ColdReset
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_RHI -l IP_ADDR_RANGE.txt -c BmcReset --action ColdReset
[SAA_HOME]# ./saa -I Remote_RHI -l IP_ADDR_RANGE.txt -c BmcReset --action WarmReset
```

## Output

```
The BMC will be reset immediately.
Please wait a few minutes for the BMC to restart.
..................................................
...................................
Done.
```

## Notes

- The `--bmc_boot_check` option is not compatible with in-band pure Redfish usage on X14/B14 systems, because resetting the BMC configuration disables the Redfish host interface by default on these systems.
- The `--bmc_boot_check` option is not supported for in-band Redfish command mode.
- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the log file created for the managed system.
