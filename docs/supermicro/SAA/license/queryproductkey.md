# QueryProductKey

Queries the node product keys that have been activated on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c QueryProductKey
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c QueryProductKey
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c QueryProductKey
```

## Options

- `--show_index`: (Optional) Prints the key index information.
- `--showall`: (Optional) Prints the key index and full key information.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c QueryProductKey
```

### In-Band
```bash
[SAA_HOME]# ./saa -c QueryProductKey

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c QueryProductKey
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c QueryProductKey
```

`SList.txt`:
```
192.168.34.56
192.168.34.57 ADMIN1 PASSWORD1
```

## Output

The console output contains one line per node product key activated on the managed system. In each line, the first field is the key name; keys have extra fields describing detailed attributes if available.

```
SFT-OOB-LIC
SFT-DCMS-SINGLE  , invoice: X8800693687A , creation date: 2019/12/03
SFT-SPM-LIC     , invoice: X8800693688A , creation date: 2019/12/04
SFT-DCMS-SVC-KEY  , invoice: X8800693689A , creation date: 2019/12/04
Number of product keys: 4
```

## Notes

- For multiple systems, if the execution "Status" field of a managed system is SUCCESS, the node product keys activated on that managed system are shown in the "Execution Message" section in the created log file.
