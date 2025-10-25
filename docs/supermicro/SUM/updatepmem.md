# UpdatePMem

## Description

Use the "UpdatePMem" command with the PMem firmware image PMem.bin to run SUM to update the PMem of managed system.

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c UpdatePMem [[--file <filename>] | [--restore_default_fw]] [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [--reboot]
```

## Options

- `--file <filename>`: Specifies the PMem firmware image file to update.
- `--restore_default_fw`: Restores the default PMem firmware.
- `--current_password <current password>`: Specifies the current BIOS password.
- `--cur_pw_file <current password file path>`: Specifies the file containing the current BIOS password.
- `--reboot`: Reboots the system after update.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePMem --file PMem.bin --reboot
```

### In-Band
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c UpdatePMem --file PMem.bin --reboot
```

```
[SUM_HOME]# ./sum -c UpdatePMem --restore_default_fw --reboot
```

## Notes

- This command is available on the X12 3rd Gen Intel® Xeon® Scalable processors with Intel® C621A Series Chipsets and later platforms.
- For more detailed usages of PMem, please contact the technical support of Supermicro.
