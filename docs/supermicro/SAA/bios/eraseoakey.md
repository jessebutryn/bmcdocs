# EraseOAKey

Erases the BIOS OA key. This command only supports in-band usage.

## Syntax

### In-Band
```
saa -c EraseOAKey [--reboot]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c EraseOAKey [--reboot] [--remote_saa <remote SAA path>]
```

## Options

- `--reboot`: Forces the managed system to reboot or power up after operation

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c EraseOAKey --reboot
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c EraseOAKey --reboot --remote_saa /root/saa
```

## Notes

- The OA key is erased only after the system is rebooted or powered up.
- This command only supports in-band usage (no OOB syntax).
