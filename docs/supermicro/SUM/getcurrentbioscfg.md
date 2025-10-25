# GetCurrentBiosCfg

## Description

Use the "GetCurrentBiosCfg" command to execute SUM to get the current BIOS settings from the managed system and save it in the USER_SETUP.file.

## Notes

- This BIOS configuration file is synchronized to the BMC from the BIOS when the system reboots or powers up.
- If the customer has flashed the BMC firmware image, this function will not work until the managed system is first rebooted or powered up.
- X11 Intel® Xeon® Scalable Processors with Intel® C620 Series Chipsets and newer platforms support HII. The current BIOS settings will be generated as XML and plain text formats for HII and DAT, respectively.
- The XML file of the BIOS configuration contains extended ASCII characters. Please use ISO 8859-1 encoding to view the BIOS configuration XML file.
- SUM 2.2.0 or later supports text-based user interface (TUI). For details, refer to 4.9 TUI.
- SUM 2.7.0 or later supports generating a compact version of the BIOS configuration file for TUI using the "--compact" option to remove the unchanged BIOS settings. To view an example of a compact configuration file, refer to Appendix G. Removing Unchanged BIOS Settings in an XML File.
- TUI does not support Remote In-band usage.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c GetCurrentBiosCfg --file <USER_SETUP.file> [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--overwrite] [--tui [--compact]]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetCurrentBiosCfg --file <USER_SETUP.file> [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--overwrite] [--remote_sum <remote sum path>]
```

## Options

- `--file <USER_SETUP.file>`: Specifies the file to save the BIOS settings.
- `--current_password <current password>`: Specifies the current BIOS password.
- `--cur_pw_file <current password file path>`: Specifies the file containing the current BIOS password.
- `--overwrite`: Overwrites the output file if it exists.
- `--tui`: Enables text-based user interface.
- `--compact`: Generates a compact version of the BIOS configuration file for TUI (removes unchanged BIOS settings).
- `--remote_sum <remote sum path>`: Specifies the path to the remote SUM executable (for Remote In-Band).

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCurrentBiosCfg --file USER_SETUP.file --overwrite
```

### In-Band
```
[SUM_HOME]# ./sum -c GetCurrentBiosCfg --file USER_SETUP.file --overwrite
```

### Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetCurrentBiosCfg --file USER_SETUP.file --overwrite --remote_sum /root/sum
```
