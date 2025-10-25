# ChangeDmiInfo

Updates DMI (Desktop Management Interface) information on the managed system using a DMI configuration file.

## Prerequisites

1. Get current DMI information (see GetDmiInfo)
2. Edit the DMI information file

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c ChangeDmiInfo --file <DMI.txt> [--reboot]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c ChangeDmiInfo --file <DMI.txt> [--reboot] [--remote_sum <remote sum path>]
```

## Options

- `--file <DMI.txt>`: Required. DMI information file
- `--reboot`: Reboot system after DMI update
- `--remote_sum <remote sum path>`: Path to remote SUM executable

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeDmiInfo --file DMI.txt --reboot
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ChangeDmiInfo --file DMI.txt --reboot
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c ChangeDmiInfo --file DMI.txt --reboot
```

## Notes

- Supported editable DMI items may vary between BIOS versions
- The version variable in DMI.txt must match the managed system's version
- Changes only take effect after system reboot or power up
- DMI information is synchronized from BIOS to BMC on reboot/power up
