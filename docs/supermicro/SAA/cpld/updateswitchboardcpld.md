# UpdateSwitchboardCpld

Updates the Main or Side (Left/Right) Switchboard CPLD with the given image file. Supported on CPLD RoT systems of X13/H13 and later platforms.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateSwitchboardCpld --file <filename> --type <type> [--index <index>] [--reboot]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateSwitchboardCpld --file <filename> --type <type> [--index <index>] [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateSwitchboardCpld --file <filename> --type <type> [--index <index>] [--reboot]
```

## Options

- `--file <file name>`: Updates the Main or Side Switchboard CPLD with the given image file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--type`: Sets action to: 1 = Main, 2 = Left, 3 = Right.
- `--individually`: (Optional) Updates each CPLD Switch Board with its corresponding configuration file individually.
- `--post_complete`: (Optional) Waits for the managed system's POST to complete after rebooting.
- `--index <number>`: (Optional) Sets the CPLD index. The default value is 1, and the index count starts from 1.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateSwitchboardCpld --file Left_Switchboard_CPLD2.jed --type Left --index 2
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateSwitchboardCpld --file Left_Switchboard_CPLD2.jed --type Left --index 2
```

## Output

```
Managed system.....................192.168.34.56
 [Left Switchboard]
 CPLD 2 version.............3F
Status: Start updating Switchboard CPLD for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW...........Done
Preparing updating FW.............Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: Switchboard CPLD is updated for 192.168.34.56
Note: Update done. No further action is needed for this firmware to take effect.
```

The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.

## Notes

- Left/Right Switchboard CPLD #1 is not supported for the user to update.
- Side Switchboard CPLD (Left or Right) firmware can be used interchangeably to update, but not for Main Switchboard as it has its own firmware.
- Reboot option is required when updating the Main Switchboard CPLD, since it can only be updated when the system is powered off. Reboot option is optional when updating Side Switchboard CPLD.
- Updating Side Switchboard CPLD requires the system to be in a fully booted up state.
- Limitation: when the system is in the process of powering up, this command can fail. Wait for the system to fully boot up and try again.
