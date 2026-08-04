# DownloadBmcCfg

Downloads the current BMC configuration file from the managed system and saves it in either text or binary file format, specified with `--format`. Both text and binary BMC configuration files are generated directly by the BMC. This is a license-free alternative to `GetBmcCfg --dump` for downloading the binary configuration file.

The BMC configuration file in text format displays the supported and editable BMC configuration elements in XML format. The binary format file can only be used to back up and restore the BMC configuration and cannot be modified.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c DownloadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml> [--overwrite]
```

### In-Band
```
saa -c DownloadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml> [--overwrite]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c DownloadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml> [--overwrite] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c DownloadBmcCfg [--format <BINARY | TEXT>] --file <BmcCfg.bin | BmcCfg.xml> [--overwrite]
```

## Options

- `--file <file name>`: Required. Downloads the BMC configuration to a file
- `--overwrite`: Overwrites the output file
- `--format <file format>`: Works with `--file` to download the BMC configuration in `BINARY` (default) or `TEXT` format

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DownloadBmcCfg --format BINARY --file BmcCfg.bin --overwrite
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DownloadBmcCfg --format TEXT --file BmcCfg.xml --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c DownloadBmcCfg --format BINARY --file BmcCfg.bin --overwrite
[SAA_HOME]# ./saa -c DownloadBmcCfg --format TEXT --file BmcCfg.xml --overwrite
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c DownloadBmcCfg --format BINARY --file BmcCfg.bin --overwrite --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c DownloadBmcCfg --format TEXT --file BmcCfg.xml --overwrite --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c DownloadBmcCfg --format BINARY --file BmcCfg.bin --overwrite
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c DownloadBmcCfg --format TEXT --file BmcCfg.xml --overwrite
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c DownloadBmcCfg --format BINARY --file BmcCfg.bin --overwrite --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c DownloadBmcCfg --format TEXT --file BmcCfg.xml --overwrite --remote_saa /root/saa
```

## Output

### Text format
```
<?xml version="1.0" encoding="UTF-8"?>
<IPMI>
 <Networking>
 <IPAddr value="192.168.034.056"/>
 <MacAddr value="aa:bb:cc:dd:ee:ff"/>
 <SubNetMask value="255.255.000.000"/>
 <DefaultGateWayAddr value="192.168.000.254"/>
 <DHCPEnable value="1"/>
 </Networking>
</IPMI>
```

## Notes

- The BMC configuration file in text format currently only supports BMC IPv4 configuration.
- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its current setting is stored in its output file, e.g., `BmcCfg.xml.192.168.34.56` or `BmcCfg.bin.192.168.34.56`. The `--overwrite` option overwrites an existing file.
