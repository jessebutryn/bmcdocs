# UpdateAocNIC

Updates the add-on NIC firmware of the managed system with the given add-on NIC firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateAocNIC {--file <filename> --dev_id <add-on NIC device ID>} [--upgrade_only] [[--reboot [--post_complete]] | [--check_reboot_required]]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c UpdateAocNIC {--file <filename> --dev_id <add-on NIC device ID>} [--upgrade_only] [[--reboot] | [--check_reboot_required]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateAocNIC {--file <filename> --dev_id <add-on NIC device ID>} [--upgrade_only] [[--reboot [--post_complete]] | [--check_reboot_required]]
```

## Options

- `--file <file name>`: Updates AOC NIC with the given add-on NIC file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--dev_id <DEVICE ID>`: Device ID of AOC NIC.
- `--post_complete`: (Optional) Waits for the managed system's POST to complete after reboot.
- `--upgrade_only`: (Optional) Firmware updates are only performed when the version is newer.
- `--check_reboot_required`: (Optional) Displays a warning message when a system reboot or power cycle is required.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateAocNIC --file AOC_NIC.bin --dev_id 1 --reboot --post_complete

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateAocNIC --file AOC_NIC.bin --dev_id 1 --upgrade_only --reboot --post_complete
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateAocNIC --file AOC_NIC.bin --dev_id 1 --reboot

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateAocNIC --file AOC_NIC.bin --dev_id 1 --check_reboot_required
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateAocNIC --file AOC_NIC.bin --dev_id 1 --reboot --post_complete
```

## Output

The execution results for the managed system are updated in the "Execution Message" section of the managed system in the created log file.

## Notes

- Use the `GetAocNICInfo` command to check the existing device IDs on the managed system.
- For updatable Add-On NIC card chipsets, refer to the package file "PlatformFeatureSupportMatrix.pdf" or contact Supermicro technical support.
