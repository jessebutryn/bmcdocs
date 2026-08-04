# RemoteKeyboard

Sends keyboard operations to the remote managed system.

## Syntax

### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c RemoteKeyboard [--file <keyboard.txt>] [--showall]
```

## Options

- `--file <file name>` (Optional): Reads keyboard operations from the specified file.
- `--showall` (Optional): Shows all supported keys and some samples.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RemoteKeyboard --file keyboard.txt

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RemoteKeyboard --showall
```

### In-Band
```bash
[SAA_HOME]# ./saa -c RemoteKeyboard --showall
```

## Notes

- `--showall` displays the supported keys for Remote Keyboard operations along with usage samples.
