# UpdatePsu

Updates the managed system with the signed PSU firmware image required by the OEM, specifying the PSU index or slave address.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdatePsu --file <filename> --address <PSU slave address>
saa -i <IP or host name> -u <username> -p <password> -c UpdatePsu [--file <filename>] --index <PSU index> --reboot [--post_complete]
```

### In-Band
```
saa -c UpdatePsu --file <filename> --address <PSU slave address>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdatePsu --file <filename> --address <PSU slave address>
saa -l <system list file> [-u <username> -p <password>] -c UpdatePsu --file [<filename>] --index <PSU index> --reboot [--post_complete]
```

## Options

- `--file <file name>`: PSU firmware file.
- `--reboot`: Forces the managed system to reboot or power up.
- `--address`: PSU module address in HEX format. Get the PSU module slave address from the `GetPsuInfo` command.
- `--post_complete`: Waits for the managed system to POST complete after a reboot.
- `--index`: PSU module index. Get the PSU module index from the `GetPsuInfo` command.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePsu --file Supermicro_PSU.x0 --address 0x80

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePsu --file Supermicro_PSU.x0 --index 1 --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePsu --index all --reboot --post_complete
```

### In-Band
```bash
[SAA_HOME]# ./saa -c UpdatePsu --file Supermicro_PSU.x0 --address 0x80
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdatePsu --file Supermicro_PSU.x0 --address 0x80
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdatePsu --index all --reboot --post_complete
```

## Output

```
Managed system...........192.168.34.56
 PSU index............1
 PSU model............PWS-5K26G-2R
 PSU FW revision......1.0.0
 PSU HW revision......1.2
Local PSU image file.....Supermicro_PSU.x0
 PSU model............PWS-5K26G-2R
 PSU FW revision......1.0.1
 PSU HW revision......1.2
Status: Start updating PSU for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW..........Done
Preparing updating PSU...Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Rebooting target system............Done
Status: PSU is updated for 192.168.34.56
WARNING: Without option --post_complete, please manually confirm the managed
system is POST complete before executing next action.
```

### With --post_complete
```
Status: The managed system 192.168.34.56 is waiting for POST complete
..................................................
..................................................
..............
Status: The managed system 192.168.34.56 is POST completed
Status: PSU is updated for 192.168.34.56
```

## Notes

- The target system must be powered off while updating PSU firmware.
- The `--index all` option can be used to update all PSUs on the system; however, all PSUs must be of the same PSU model and PSU hardware version.
- The `--index` option can be used without the `--file` option, provided that the PSU firmware image is placed in the designated directory within SAA. Example: `<SAApath>/<PSU model name>/<PSU HW revision>/<PSU firmware image>`.
- The `--reboot` and `--post_complete` options are only supported when using the `--index` option.
- If the execution Status field of the managed system shows SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
