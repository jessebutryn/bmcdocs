# SetBootOption

Sets the boot options for the target system, including NextBootOnly, BypassPassword, and Device Type settings. If `--next_boot_only` and `--bypass_password` are not used, the default value is "Disable." After executing this command, no power operations are performed unless the `--action` option is used, in which case a power operation is carried out.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetBootOption --device_type <Device Type ID> [--next_boot_only <Enable | Disable>] [--bypass_password <Enable | Disable>] [--action <action> [--post_complete]]
```

### In-Band
```
saa -c SetBootOption --device_type <Device Type ID> [--next_boot_only <Enable | Disable>] [--bypass_password <Enable | Disable>] [--action <action>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetBootOption --device_type <Device Type ID> [--next_boot_only <Enable | Disable>] [--bypass_password <Enable | Disable>] [--action <action> [--post_complete]]
```

## Options

- `--device_type <Device Type ID>`: Sets the boot device type. For Legacy Device: `0` = No Override, `1` = PXE, `2` = Hard Drive, `3` = CD DVD, `4` = BIOS Setup, `5` = USB Key, `6` = Virtual USB Hard Drive, `7` = Virtual Floppy, `8` = ISO Image. For UEFI Device: `9` = UEFI: Hard Drive, `10` = UEFI: CD DVD, `11` = UEFI: USB Key, `12` = Virtual UEFI: USB Hard Drive, `13` = UEFI: ISO Image, `14` = UEFI: PXE, `15` = UEFI: Floppy|Virtual Floppy, `16` = UEFI: BIOS Shell
- `--action <action>`: Sets power action to `0` = up, `1` = down, `2` = cycle, `3` = reset, `4` = softshutdown, `5` = reboot
- `--post_complete`: Waits for the managed system's POST to complete after rebooting
- `--next_boot_only <Enable/Disable>`: Sets NextBootOnly status (default: Enable)
- `--bypass_password <Enable/Disable>`: Sets ByPassWord status (default: Disable)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBootOption --device_type 0 --next_boot_only Enable --bypass_password Enable --action 5
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SetBootOption --device_type 0 --next_boot_only Enable --bypass_password Enable --action 5
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBootOption --device_type 0 --next_boot_only Enable --bypass_password Enable --action 5
```

## Notes

- If the execution "Status" field for a managed system is SUCCESS, the BIOS and BMC capabilities of the managed system will be shown in the "Execution Message" section in the created log file.
