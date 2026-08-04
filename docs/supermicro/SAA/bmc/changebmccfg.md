# ChangeBmcCfg

Updates the BMC with the given configuration file, or restores the BMC configuration from a read-only binary configuration file with `--restore`.

## Prerequisites

1. Select one managed system as the golden sample for current BMC settings (for multiple systems).
2. Get the current BMC settings (see `GetBmcCfg`).
3. Edit the configurable element values in the BMC configuration text file `BmcCfg.xml` to the desired values.
4. Optionally skip unchanged tables by setting the `Action` attribute to "None".
5. Optionally remove unchanged tables/elements in the text file.

For uploading a binary BMC configuration file with `--restore`, the license-free `UploadBmcCfg` command is also available (see `UploadBmcCfg`).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeBmcCfg --file <BmcCfg.xml> [--skip_unknown]
saa -i <IP or host name> -u <username> -p <password> -c ChangeBmcCfg --restore --file <BmcCfg.bin>
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c ChangeBmcCfg --file <BmcCfg.xml> [--skip_unknown]
saa -I Redfish_HI -u <username> -p <password> -c ChangeBmcCfg --restore --file <BmcCfg.bin>
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c ChangeBmcCfg --file <BmcCfg.xml> [--skip_unknown] [--remote_saa <remote SAA path>]
saa -I Remote_RHI -u <username> -p <password> --oi <OS IP address> --ou <OS username> --op <OS password> -c ChangeBmcCfg --restore --file <BmcCfg.bin> [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeBmcCfg --file <BmcCfg.xml> [--skip_unknown] [--individually]
saa -l <system list file> [-u <username> -p <password>] -c ChangeBmcCfg --restore --file <BmcCfg.bin> [--individually]
```

## Options

- `--file <file name>`: Required. Updates the BMC with the given configuration file
- `--restore`: Restores the BMC configuration with the corresponding read-only configuration file
- `--individually`: Updates each BMC with the corresponding configuration file individually
- `--skip_unknown`: Skips the unknown tables or settings in the BMC configuration file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBmcCfg --file BmcCfg.xml
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeBmcCfg --restore --file BmcCfg.bin
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeBmcCfg --file BmcCfg.xml
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c ChangeBmcCfg --restore --file BmcCfg.bin
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c ChangeBmcCfg --file BmcCfg.xml --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_RHI --oi 192.168.34.56 --ou root --op 111111 -u ADMIN -p PASSWORD -c ChangeBmcCfg --restore --file BmcCfg.bin --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeBmcCfg --file BmcCfg.xml
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeBmcCfg --restore --file BmcCfg.bin --individually
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c ChangeBmcCfg --file BmcCfg.xml --individually --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c ChangeBmcCfg --restore --file BmcCfg.bin --individually --remote_saa /root/saa
```

### Updating BMC settings after firmware update, dumped with GetBmcCfg
```bash
[SAA_HOME]# ./saa -c ChangeBmcCfg --file BmcCfg.xml --overwrite
```

## Output

```
Status: Start updating the BMC configuration for 192.168.34.56
************************************WARNING************************************
 Do not remove AC power from the server.
*******************************************************************************
..................................
Status: The BMC configuration is updated for 192.168.34.56
```

## Notes

- Pay attention when modifying content inside the `<LAN>` XML element — the connection could be broken if the LAN configuration is changed.
- For in-band operation, all data of the `<Configurations>` element inside `<LAN>` is configurable. For OOB operation, if Redfish is not supported, all configurations inside `<LAN>` are read only, and the `<DynamicIPv6>`/`<StaticIPv6>` elements are always read only for OOB.
- For OOB operation, if the BMC supports account lockout configuration, the `<Account>` table replaces the `<UserManagement>` table.
- SAA supports pure Redfish LAN tables in the BMC configuration.
- If the execution "Status" field for a managed system is SUCCESS, its BMC settings are updated. To restore multiple systems individually, provide `BmcCfg.bin.192.168.34.56` and `BmcCfg.bin.192.168.34.57`, set `--file` to `BmcCfg.bin`, and use `--individually`; SAA searches for the per-system files.
- To install a BMC identity certification, use the `<Certification>` element inside the BMC configuration XML file (see `GetBmcCfg` notes for the XML structure); the BMC resets after the certificate file is uploaded.
