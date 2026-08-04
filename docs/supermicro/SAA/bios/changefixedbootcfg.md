# ChangeFixedBootCfg

Updates the BIOS fixed boot order with the given configuration file.

## Prerequisites

1. Get the fixed boot configuration (see `GetFixedBootCfg`).
2. Edit the item/variable values in the USER_SETUP.file to the desired values.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeFixedBootCfg --file <USER_SETUP.file> [--reboot [--post_complete]] --redfish
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c ChangeFixedBootCfg --file <USER_SETUP.file> [--reboot] --redfish
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeFixedBootCfg --file <USER_SETUP.file> [--reboot [--post_complete]] [--individually] --redfish
```

## Options

- `--file <file name>`: Required. Updates the BIOS fixed boot order with the given configuration file
- `--redfish`: Updates the BIOS fixed boot order with the pure Redfish solution
- `--reboot`: Forces the managed system to reboot or power up after operation
- `--individually`: Updates each fixed BIOS boot configuration individually with the corresponding configuration file
- `--post_complete`: Waits for the managed system's POST to complete after reboot

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeFixedBootCfg --redfish --file USER_SETUP.file --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c ChangeFixedBootCfg --redfish --file USER_SETUP.file --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l Slist.txt -u ADMIN -p PASSWORD -c ChangeFixedBootCfg --file USER_SETUP.file --reboot --redfish
[SAA_HOME]# ./saa -l Slist.txt -u ADMIN -p PASSWORD -c ChangeFixedBootCfg --file USER_SETUP.file --reboot --individually --redfish
```

## Notes

- Unchanged settings can be deleted to skip the update.
- The XML version line and the `<FixedBootCfg>` root should not be deleted.
- The On/Off boot device can be modified in the `<xxxxxBBSPriorities><setting>` menu; if the boot device is on the boot order list, it cannot be disabled there — disable it in the boot order first, then in the `<xxxxxBBSPriorities><setting>` menu.
- If more than one device is listed on the `<xxxxxBBSPriorities><setting>` menu, changing their order there also changes the boot order shown in the "Fixed Boot Order" menu for that selected option, but the UEFI Network display device cannot be changed directly in the "Fixed Boot Order" menu.
- The change takes effect after the managed system is rebooted.
- Use `--individually` to update each managed system with the corresponding configuration file: provide `USER_SETUP.file.192.168.34.56` and `USER_SETUP.file.192.168.34.57`, set `--file` to `USER_SETUP.file`, and SAA searches for the per-system files.
