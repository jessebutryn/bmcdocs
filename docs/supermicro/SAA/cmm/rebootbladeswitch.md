# RebootBladeSwitch

Reboots a managed switch module.

## Syntax

### OOB
```
saa -i <Switch IP or switch host name> -u <Switch username> -p <Switch password> -c RebootBladeSwitch
saa -i <CMM IP or CMM host name> -u <CMM username> -p <CMM password> -c RebootBladeSwitch --dev_id <Switch device ID> --switch_user <Switch username> --switch_pw <Switch password>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <Switch username> -p <Switch password>] -c RebootBladeSwitch
saa -l <system list file> [-u <username> -p <password>] -c RebootBladeSwitch [--dev_id <Switch device ID> --switch_user <Switch username> --switch_pw <Switch password>]
```

## Options

- `--switch_user <Switch user ID>`: Assigns switch user when updating through CMM.
- `--switch_pw <Switch user password>`: Assigns switch password when updating through CMM.
- `--dev_id <Device ID>`: Assigns switch index when updating through CMM. Switch index: `[A1,A2,B1,B2]` or `[ALL]`.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RebootBladeSwitch
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RebootBladeSwitch --dev_id A1 --switch_user ADMIN --switch_pw ADMIN
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SwitchList.txt -u ADMIN -p PASSWORD -c RebootBladeSwitch
[SAA_HOME]# ./saa -l SwitchList.txt -u ADMIN -p PASSWORD -c RebootBladeSwitch --dev_id A1 --switch_user ADMIN --switch_pw ADMIN
```

## Notes

- SBM-25G-P10 and BMB-25G-P10 are the same switch module.
- This command is only available for switch modules SBM-25G-P10/BMB-25G-P10/MBM-XEM-002/MBM-GEM-004/SBM-25G-100.
- Minimum supported firmware versions: SBM-25G-100/BMB-25G-P10 &ge; 1.0.0.10, MBM-XEM-002 &ge; 2.2.1.34, MBM-GEM-004 &ge; 1.3.0.8, SBM-25G-100 &ge; 1.4.0.11.
- To reboot the managed switch through a CMM IP and switch device ID, use the `--dev_id`, `--switch_user`, and `--switch_pw` options. Use `GetBladeSwitchInfo` to get the switch device ID.
