# SetLockdownMode

Sets the BMC system to Lockdown Mode on the managed system. When System Lockdown Mode is enabled, neither setting configurations nor updating firmware is allowed.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetLockdownMode {--lock <yes | no>} [--reboot [--post_complete]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetLockdownMode {--lock <yes | no>} [--reboot [--post_complete]]
```

## Options

- `--lock <yes/no>`: Locks/unlocks the managed system.
- `--reboot` (Optional): Forces the managed system to reboot or power up after operation.
- `--post_complete` (Optional): Waits for the managed system's POST to complete after reboot.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetLockdownMode --lock <yes | no> --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetLockdownMode --lock <yes | no> --reboot
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```
