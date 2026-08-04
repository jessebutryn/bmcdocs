# UpdateBladeSwitch

Updates the firmware of a managed switch module with the given switch firmware image.

## Syntax

### OOB
```
saa -i <Switch IP or switch host name> -u <Switch username> -p <Switch password> -c UpdateBladeSwitch --file <filename> [--reboot]
saa -i <CMM IP or CMM host name> -u <CMM username> -p <CMM password> -c UpdateBladeSwitch --file <filename> --dev_id <Switch device ID> --switch_user <Switch username> --switch_pw <Switch password> [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <Switch username> -p <Switch password>] -c UpdateBladeSwitch --file <filename> [--reboot] [--individually]
saa -l <system list file> [-u <username> -p <password>] -c UpdateBladeSwitch --file <filename> [--dev_id <Switch device ID> --switch_user <Switch username> --switch_pw <Switch password>] [--reboot] [--individually]
```

## Options

- `--switch_user <Switch user ID>`: Assigns switch user when updating through CMM.
- `--switch_pw <Switch user password>`: Assigns switch password when updating through CMM.
- `--reboot`: Forces the switch to reboot or power up after operation.
- `--individually`: Updates each switch module with the corresponding firmware image individually.
- `--dev_id <Device ID>`: Assigns switch index when updating through CMM. Switch index: `[A1,A2,B1,B2]` or `[ALL]`.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBladeSwitch --file Supermicro_Switch.bin --reboot
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBladeSwitch --file Supermicro_Switch.bin --dev_id A1 --switch_user ADMIN --switch_pw ADMIN --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SwitchList.txt -u ADMIN -p PASSWORD -c UpdateBladeSwitch --file Supermicro_Switch.bin --reboot
[SAA_HOME]# ./saa -l SwitchList.txt -u ADMIN -p PASSWORD -c UpdateBladeSwitch --file Supermicro_Switch.bin --reboot --individually
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateBladeSwitch --file Supermicro_Switch.bin --dev_id A1 --switch_user ADMIN --switch_pw ADMIN --reboot
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateBladeSwitch --file Supermicro_Switch.bin --dev_id A1 --switch_user ADMIN --switch_pw ADMIN --reboot --individually
```

## Notes

- SBM-25G-P10 and BMB-25G-P10 are the same switch module.
- This command is only available for switch modules SBM-25G-P10/BMB-25G-P10/MBM-XEM-002/MBM-GEM-004/SBM-25G-100.
- Minimum supported firmware versions: SBM-25G-100/BMB-25G-P10 &ge; 1.0.0.10, MBM-XEM-002 &ge; 2.2.1.34, MBM-GEM-004 &ge; 1.3.0.8, SBM-25G-100 &ge; 1.4.0.11.
- The switch module must be rebooted for the update to take effect. Without `--reboot`, the switch module will not restart after this command is executed — use `RebootBladeSwitch` to reboot it separately.
- To update switch firmware through a CMM IP and switch device ID, use the `--dev_id`, `--switch_user`, and `--switch_pw` options. Use `GetBladeSwitchInfo` to get the switch device ID.
- For `--individually` usage across multiple systems (e.g., 192.168.34.100 and 192.168.34.101), provide two files named Supermicro_Switch.bin.192.168.34.100 and Supermicro_Switch.bin.192.168.34.101, and set `--file` to `Supermicro_Switch.bin`. SAA searches for the per-system files to update each system respectively.
