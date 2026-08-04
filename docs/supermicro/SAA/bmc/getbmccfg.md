# GetBmcCfg

Gets the current BMC settings from the managed system and saves them in a BmcCfg.xml file, or in a BmcCfg.bin file with the `--dump` option.

For downloading the binary BMC configuration file, the license-free `DownloadBmcCfg` command is also available (see `DownloadBmcCfg`).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBmcCfg --file <BmcCfg.xml> [--overwrite]
saa -i <IP or host name> -u <username> -p <password> -c GetBmcCfg --dump --file <BmcCfg.bin> [--overwrite]
```

### In-Band
```
saa [-I Redfish_HI [-u <username> -p <password>]] -c GetBmcCfg [--file <BmcCfg.xml>] [--overwrite]
saa -I Redfish_HI [-u <username> -p <password>] -c GetBmcCfg --dump --file <BmcCfg.bin> [--overwrite]
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c GetBmcCfg --file <BmcCfg.xml> [--overwrite] [--remote_saa <remote SAA path>]
saa -I Remote_RHI -u <username> -p <password> --oi <OS IP address> --ou <OS username> --op <OS password> -c GetBmcCfg --dump --file <BmcCfg.bin> [--overwrite] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBmcCfg --file <BmcCfg.xml> [--overwrite]
saa -l <system list file> [-u <username> -p <password>] -c GetBmcCfg --dump --file <BmcCfg.bin> [--overwrite]
```

## Options

- `--file <file name>`: Saves the configuration to a file (prints on screen if the file-saving function is not available)
- `--dump`: Dumps a read-only BMC configuration file (binary)
- `--overwrite`: Overwrites the output file
- `--sample_file <config_format.xml>`: Creates the BMC configuration using the table format from the sample file (X13/H13 or later platforms only)
- `--action`: Sets the action of each XML table; acceptable values are `None` or `Change`

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcCfg --file BmcCfg.xml --overwrite
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcCfg --dump --file BmcCfg.bin --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetBmcCfg --file BmcCfg.xml --overwrite
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetBmcCfg --dump --file BmcCfg.bin --overwrite
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetBmcCfg --file BmcCfg.xml --overwrite --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_RHI --oi 192.168.34.56 --ou root --op 111111 -u ADMIN -p PASSWORD -c GetBmcCfg --dump --file BmcCfg.bin --overwrite --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBmcCfg --file BmcCfg.xml --overwrite
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBmcCfg --dump --file BmcCfg.bin --overwrite
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetBmcCfg --file BmcCfg.xml --overwrite --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c GetBmcCfg --file BmcCfg.xml --overwrite --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c GetBmcCfg --dump --file BmcCfg.bin --overwrite --remote_saa /root/saa
```

### Generating BMC settings format based on a sample file (X13/H13 or later)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcCfg --file BmcCfg.xml --overwrite --sample_file config_format.xml
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBmcCfg --file BmcCfg.xml --overwrite --sample_file config_format.xml
```

## Notes

- Received tables/elements may not be identical between two managed systems; only the tables/elements supported for the managed system will be received.
- For in-band and OOB usage, file formats for getting BMC settings may differ — be careful not to misuse them.
- SAA gets/changes the syslog table in the BMC configuration through HTTPS, so syslog information will be lost if HTTPS is disabled.
- For OOB operation, if the BMC supports account lockout configuration, the `<Account>` table replaces the `<UserManagement>` table.
- SAA supports pure Redfish LAN tables in the BMC configuration.
- The `--sample_file` option only supports X13/H13 or later platforms. Do not remove table fields in the sample file — if a table version in the sample file cannot be recognized, that table will not be generated.
- To install a BMC identity certification, edit the `<Certification>` element in the BMC configuration XML file (obtained via this command) and apply it with `ChangeBmcCfg`. Set `<CertFile>` to the certificate file path (e.g. `/home/test/cert.pem`) and `<PrivKeyFile>` to the private key file path (e.g. `/home/test/key.pem`); the BMC will reset after the file is uploaded. Example:
    ```xml
    <Certification Action="Change">
     <!--Supported Action:None/Change-->
     <Information>
     <CertStartDate>Jul 27 00:00:00 2018 GMT</CertStartDate>
     <CertEndDate>Jul 27 00:00:00 2021 GMT</CertEndDate>
     </Information>
     <Configuration>
     <!--Configurations for BMC certifications-->
     <CertFile>/home/test/cert.pem</CertFile>
     <!--string value; path to file-->
     <PrivKeyFile>/home/test/key.pem</PrivKeyFile>
     <!--string value; path to file-->
     <!--BMC will be reset after uploading this file-->
     </Configuration>
    </Certification>
    ```
- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its current setting is stored in its output file, e.g., `BmcCfg.xml.192.168.34.56` or `BmcCfg.bin.192.168.34.56`. The `--overwrite` option overwrites an existing file.
