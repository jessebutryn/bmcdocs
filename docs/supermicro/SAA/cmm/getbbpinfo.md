# GetBbpInfo

Gets the BBP (Blade Backplane) firmware image and its information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBbpInfo [--file <filename>]
```

### In-Band
```
saa -c GetBbpInfo [--file_only <filename>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBbpInfo [--file <filename>]
```

## Options

- `--file <file name>`: Reads the BBP information from an input BBP image file.
- `--file_only`: Works with the `--file` option, and only reads BBP information from the input image file (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBbpInfo --file BBP.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBbpInfo --file BBP.bin
```

## Output

```
Managed system...........192.168.34.56
 BBP version..........01.08
Local BBP image file.....BBP_EC_2019-03-14_1901.47v1.08.bin
 BBP version..........01.08
```

## Notes

- If the Status field for a managed system shows SUCCESS, the BBP information of the managed system will be shown in the Execution Message section of the created log file.
