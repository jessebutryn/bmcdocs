# GetVROCCfg

Gets the current VROC settings from the managed system and saves them to a VROC.cfg.xml file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetVROCCfg --file <filename> [--overwrite]
```

### In-Band
```
saa -c GetVROCCfg --file <filename> [--overwrite]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetVROCCfg --file <filename> [--overwrite]
```

## Options

- `--current_password <current password>`: Checks the current BIOS Administrator password (optional).
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password (optional).
- `--post_complete`: Waits for the managed system's POST to complete after reboot (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetVROCCfg --file VROC.cfg.xml
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetVROCCfg --file VROC.cfg.xml --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetVROCCfg --file VROC.cfg.xml --overwrite
```

## Notes

- The received tables/elements between two managed systems might not be identical. Only the supported tables/elements for the managed system will be received.
- "NVME Mode Switch" in the BIOS setting needs to be set to "VMD" in order to use `GetVROCCfg`.
- Host software in the target system OS is required for VROC-related commands.
- The target system needs to boot into the OS in order to use VROC-related commands.
- VROC-related commands have been tested on Red Hat Enterprise Linux 8.1.
- If the execution Status field for a managed system (e.g., 192.168.34.56) is SUCCESS, its current settings are stored in its output file, e.g., VROC.cfg.xml.192.168.34.56. The `--overwrite` option forces the overwrite of an existing file of that name.
