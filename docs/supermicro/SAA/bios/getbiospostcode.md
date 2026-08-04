# GetBiosPostCode

Gets the BIOS POST code from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBiosPostCode
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetBiosPostCode
```

### Remote In-Band
```
saa -I Remote_RHI -u <username> -p <password> --oi <OS IP address> --ou <OS username> --op <OS password> -c GetBiosPostCode [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBiosPostCode
```

## Options

- `--redfish`: Uses the Redfish Host Interface for in-band get BIOS POST code (only in-band usage is supported)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBiosPostCode
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetBiosPostCode
```

### Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p ADMIN --oi 192.168.34.56 --ou root --op 111111 -c GetBiosPostCode --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBiosPostCode
```

### Multiple Systems Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c GetBiosPostCode
```

## Output

```
The BIOS POST code : 9e
```
