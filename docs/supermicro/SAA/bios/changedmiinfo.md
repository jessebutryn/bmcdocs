# ChangeDmiInfo

Updates DMI (Desktop Management Interface) information on the managed system using a DMI configuration file.

## Prerequisites

1. Get current DMI information (see `GetDmiInfo`) or edit it with `EditDmiInfo`.
2. Edit the item/variable values in the DMI.txt file to the desired values.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeDmiInfo {--file <DMI.txt>} [--reboot [--post_complete]]
```

### In-Band
```
saa -c ChangeDmiInfo {--file <DMI.txt>} [--reboot]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c ChangeDmiInfo {--file <DMI.txt>} [--reboot] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeDmiInfo {--file <DMI.txt>} [--reboot [--post_complete]] [--individually]
```

## Options

- `--file <file name>`: Required. Updates the DMI information with the given text file
- `--reboot`: Forces the managed system to reboot or power up after operation
- `--individually`: Individually updates each piece of DMI information with its corresponding text file
- `--post_complete`: Waits for the managed system's POST to complete after reboot

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeDmiInfo --file DMI.txt --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeDmiInfo --file DMI.txt --reboot
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c ChangeDmiInfo --file DMI.txt --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeDmiInfo --file DMI.txt --reboot
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeDmiInfo --file DMI.txt --reboot --individually
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c ChangeDmiInfo --file DMI.txt --reboot
```

## Notes

- The supported editable DMI items may change for different BIOS versions. The version variable of the DMI.txt file must be the same as that of the managed system and should not be edited.
- The uploaded information only takes effect after a system reboot or power up.
- To update multiple systems individually, provide `DMI.txt.<IP>` per system (e.g. `DMI.txt.192.168.34.56` and `DMI.txt.192.168.34.57`), set `--file` to `DMI.txt`, and use `--individually`; SAA searches for the per-system files to update each respective system.
