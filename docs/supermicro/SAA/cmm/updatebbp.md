# UpdateBbp

Updates the BBP (Blade Backplane) firmware of the managed system with the given BBP firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateBbp --file <filename> [--skip_check]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateBbp --file <filename> [--skip_check]
```

## Options

- `--file <file name>`: Updates the BBP with the given image file.
- `--skip_check`: Skips the Blade power status check to force update BBP (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBbp --file BBP.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateBbp --file BBP.bin
```

## Notes

- It is recommended that all system units be turned off before updating BBP. If you need to update BBP while system units are powered on, ensure enough power is being provided, and use `--skip_check` to force the update. If power is insufficient while updating BBP, the Blade system may shut down.
- The execution progress is continuously updated in the Execution Message section of the created log file.
