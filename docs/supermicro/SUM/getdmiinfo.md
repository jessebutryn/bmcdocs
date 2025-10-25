# GetDmiInfo

## Description

Use the "GetDmiInfo" command to execute SUM to get the current supported editable DMI information from the managed system and save it in the DMI.txt file.

## Notes

- This DMI file is synchronized to BMC from BIOS when the system reboots or powers up.
- If the customer has flashed a BMC firmware image, this function will not work until the managed system is first rebooted or powered up.
- The supported editable DMI items could vary from BIOS to BIOS. SUM will only show supported items.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c GetDmiInfo --file <DMI.txt> [--overwrite]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetDmiInfo --file <DMI.txt> [--overwrite] [--remote_sum <remote sum path>]
```

## Options

- `--file <DMI.txt>`: Specifies the file to save the DMI information.
- `--overwrite`: Overwrites the output file if it exists.
- `--remote_sum <remote sum path>`: Specifies the path to the remote SUM executable (for Remote In-Band).

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetDmiInfo --file DMI.txt --overwrite
```

### In-Band
```
[SUM_HOME]# ./sum -c GetDmiInfo --file DMI.txt --overwrite
```

### Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetDmiInfo --file DMI.txt --overwrite --remote_sum /root/sum
```
