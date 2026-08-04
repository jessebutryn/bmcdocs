# GetBmcLANCfg

Gets the current BMC LAN settings from the managed system and saves them in a BMCLANCfg.xml file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBmcLANCfg [--file <BMCLANCfg.xml> [--overwrite]]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetBmcLANCfg [--file <BMCLANCfg.xml> [--overwrite]]
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c GetBmcLANCfg [--file <BMCLANCfg.xml> [--overwrite]] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBmcLANCfg [--file <BMCLANCfg.xml> [--overwrite]]
```

## Options

- `--file <file name>`: Saves the configuration to a file (prints on screen if the file-saving function is not available)
- `--overwrite`: Overwrites the output file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcLANCfg --file BmcCfg.xml --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite
```

### Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.57 --ou root --op 111111 -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite
```

## Notes

- The received tables/elements might not be identical between two managed systems; only supported tables/elements for the managed system will be received.
- For in-band and OOB usage, file formats for getting BMC LAN settings may differ — be careful not to misuse them.
- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its current settings are saved in an output file, e.g., `BMCLANCfg.xml.192.168.34.56`. The `--overwrite` option overwrites an existing file.
