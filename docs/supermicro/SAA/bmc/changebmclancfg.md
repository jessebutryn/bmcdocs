# ChangeBmcLANCfg

Updates the BMC LAN configuration with the given configuration file.

## Prerequisites

1. Select one managed system as the golden sample for current BMC LAN settings (for multiple systems).
2. Get the current BMC LAN settings (see `GetBmcLANCfg`).
3. Edit the configurable element values in the `BMCLANCfg.xml` file to the desired values.
4. Optionally skip unchanged tables by setting the `Action` attribute to "None".
5. Optionally remove unchanged tables/elements in the text file.
6. Note that the IPv4 settings `IPAddr`, `SubNetmask`, `DefaultGateWayAddr` in the IPv4 table cannot be applied identically to each managed system (for multiple systems); use `--individually` to update each managed system with its corresponding configuration file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeBmcLANCfg --file <BMCLANCfg.xml> [--skip_unknown]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c ChangeBmcLANCfg --file <BMCLANCfg.xml> [--skip_unknown]
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c ChangeBmcLANCfg --file <BMCLANCfg.xml> [--skip_unknown] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeBmcLANCfg --file <BMCLANCfg.xml> [--skip_unknown] [--individually]
```

## Options

- `--file <file name>`: Required. Updates the BMC LAN configuration with the given file
- `--skip_unknown`: Skips the unknown tables or settings in the BMC LAN configuration file
- `--individually`: Updates each managed system individually with its corresponding configuration file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBmcLANCfg --file BmcCfg.xml
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeBmcLANCfg --file BMCLANCfg.xml --overwrite
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c ChangeBmcLANCfg --file BMCLANCfg.xml
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c ChangeBmcLANCfg --file BMCLANCfg.xml --overwrite
```

### Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.57 --ou root --op 111111 -c ChangeBmcLANCfg --file BMCLANCfg.xml --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeBmcLANCfg --file BMCLANCfg.xml
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeBmcLANCfg --file BMCLANCfg.xml --individually
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c ChangeBmcLANCfg --file BMCLANCfg.xml
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c ChangeBmcLANCfg --file BMCLANCfg.xml --individually
```

## Notes

- Pay attention when modifying content inside the `<LAN>` XML element — the connection could be broken if the LAN configuration is changed.
- For in-band operation, all data of the `<Configurations>` element inside `<LAN>` is configurable. For OOB operation, if Redfish is not supported, all configurations inside `<LAN>` are read only, and the `<DynamicIPv6>`/`<StaticIPv6>` elements are always read only for OOB.
- If the execution "Status" field for a managed system is SUCCESS, its BMC LAN settings are updated. To update multiple systems individually, provide `BMCLANCfg.xml.192.168.34.56` and `BMCLANCfg.xml.192.168.34.57`, set `--file` to `BMCLANCfg.xml`, and use `--individually`; SAA searches for the per-system files.
