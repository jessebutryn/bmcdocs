# RestoreFruInfo

Restores FRU (Field Replaceable Unit) information on the managed system from a previously dumped FRU file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c RestoreFruInfo --file <filename> [--format <file format>]
```

### In-Band
```
saa -c RestoreFruInfo --file <filename> [--format <file format>]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c RestoreFruInfo --file <filename> [--format <file format>] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c RestoreFruInfo --file <filename> [--format <file format>] [--individually]
```

### Multiple Systems Remote In-Band
```
saa -I Remote_INB -l <system list file> -c RestoreFruInfo --file <filename> [--format <file format>] [--individually] [--remote_saa <remote saa path>]
```

## Options

- `--file <filename>`: Reads the dumped FRU file.
- `--format <file format>`: (Optional) Works with `--file` to read a FRU file in one of the following formats: `BINARY` (default) or `TEXT`.
- `--individually`: (Optional) Restores each BMC with its corresponding FRU info file individually.
- `--remote_saa <remote SAA path>`: (Optional) Path to the remote SAA executable, for Remote In-Band usage.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RestoreFruInfo --file dumpedFile --format BINARY
```

### In-Band
```bash
[SAA_HOME]# ./saa -c RestoreFruInfo --file dumpedFile
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c RestoreFruInfo --file dumpedFile --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c RestoreFruInfo --file dumpedFile --format TEXT

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c RestoreFruInfo --file dumpedFile --format BINARY --individually
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c RestoreFruInfo --file dumpedFile --format TEXT --individually
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Notes

- To update 192.168.34.56 and 192.168.34.57, provide two files, `dumpedFile.192.168.34.56` and `dumpedFile.192.168.34.57`, and pass `--file dumpedFile`. With `--individually`, SAA searches for `dumpedFile.192.168.34.56` and `dumpedFile.192.168.34.57` to restore each system respectively.
