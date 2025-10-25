# EraseOAKey

Erases the BIOS OA (Ownership Authentication) key on the managed system.

## Syntax

### In-Band
```
sum -c EraseOAKey [--reboot]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c EraseOAKey [--reboot] [--remote_sum <remote sum path>]
```

## Options

- `--reboot`: Reboot system after erasing OA key
- `--remote_sum <remote sum path>`: Path to remote SUM executable

## Examples

### In-Band
```bash
[SUM_HOME]# ./sum -c EraseOAKey --reboot
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c EraseOAKey --reboot --remote_sum /root/sum
```

## Notes

- OA keys are erased only after system reboot or power up
- In-band usage only
- Part of BIOS management functions