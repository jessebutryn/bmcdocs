# UploadBmcCfg

Uploads a BMC configuration file (binary or text) to the managed system. This is a license-free alternative to `ChangeBmcCfg --restore` for uploading a binary configuration file, and can also upload a text/XML configuration file.

## Prerequisites

1. Download the BMC configuration file in binary or text format (see `DownloadBmcCfg`).
2. If binary, the file is not editable and can only be used to restore the BMC configuration. If text, edit the configurable element values in the XML file to the desired values.
3. Use this command with `--format BINARY` to restore from a binary file, or `--format TEXT` to update from an XML file.
4. After the configuration file is uploaded, the BMC automatically resets. Wait for the BMC to boot up before proceeding with further actions.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UploadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml>
```

### In-Band
```
saa -c UploadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml>
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c UploadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml> [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UploadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml> [--individually]
```

## Options

- `--file <file name>`: Required. Uploads the BMC configuration to the managed system
- `--individually`: Uploads each BMC with the corresponding configuration file individually
- `--format <file format>`: Works with `--file` to upload the BMC configuration in `BINARY` (default) or `TEXT` format

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UploadBmcCfg --format BINARY --file BmcCfg.bin
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UploadBmcCfg --format TEXT --file BmcCfg.xml
```

### In-Band
```bash
[SAA_HOME]# ./saa -c UploadBmcCfg --format BINARY --file BmcCfg.bin
[SAA_HOME]# ./saa -c UploadBmcCfg --format TEXT --file BmcCfg.xml
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c UploadBmcCfg --format BINARY --file BmcCfg.bin --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c UploadBmcCfg --format TEXT --file BmcCfg.xml --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UploadBmcCfg --format BINARY --file BmcCfg.bin --individually
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UploadBmcCfg --format TEXT --file BmcCfg.xml
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c UploadBmcCfg --format BINARY --file BmcCfg.bin --individually --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c UploadBmcCfg --format TEXT --file BmcCfg.xml --remote_saa /root/saa
```

## Notes

- Pay attention when modifying content inside the `<LAN>` XML element — the connection could be broken if the LAN configuration is changed.
- For in-band operation, all data of the `<Configurations>` element inside `<LAN>` is configurable. For OOB operation, if Redfish is not supported, all configurations inside `<LAN>` are read only, and the `<DynamicIPv6>`/`<StaticIPv6>` elements are always read only for OOB.
- For OOB operation, if the BMC supports account lockout configuration, the `<Account>` table replaces the `<UserManagement>` table.
- SAA supports pure Redfish LAN tables in the BMC configuration.
- If the execution "Status" field for a managed system is SUCCESS, its BMC settings are updated. To restore multiple systems individually, provide `BmcCfg.bin.192.168.34.56` and `BmcCfg.bin.192.168.34.57`, set `--file` to `BmcCfg.bin`, and use `--individually`; SAA searches for the per-system files.
