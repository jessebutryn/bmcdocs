# GetBootOption

Gets the boot option from the target system, including NextBootOnly, BypassPassword, and Device Type.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBootOption
```

### In-Band
```
saa -c GetBootOption
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBootOption
```

## Examples

### OOB
```bash
./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBootOption
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetBootOption
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBootOption
```

## Output

```
 NextBootOnly..............Enable
 BypassPassword............Disable
 DeviceType................0:No Override
```

## Notes

- If the execution "Status" field for a managed system is SUCCESS, the BIOS and BMC capabilities of the managed system will be shown in the "Execution Message" section in the created log file.
