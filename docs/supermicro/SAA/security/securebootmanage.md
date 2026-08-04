# SecureBootManage

Manages Secure Boot on the managed system through the BMC Redfish API: getting or setting secure boot status, and uploading, showing, resetting, or deleting secure boot keys. Only available on X13/H13 and later platforms; requires the SFT-DCMS-SINGLE license.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SecureBootManage --redfish --action <action> [--file_type <file type> [--file <CertificateFile>]] [--reboot [--post_complete]]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c SecureBootManage --redfish --action <action> [--file_type <file type> [--file <CertificateFile>]] [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SecureBootManage --redfish --action <action> [--file_type <file type> [--file <CertificateFile>]] [--individually] [--reboot [--post_complete]]
```

## Actions

- **Status**: Gets the system secure boot status from the BMC Redfish API.
- **Enable / Disable**: Sets the system secure boot pending status through the BMC Redfish API. Requires a system reboot to take effect.
- **Showdatabases**: Gets the information of specified system secure boot keys through the BMC Redfish API, using `--file_type`. Without `--file_type`, shows the number of all system secure boot keys.
- **UploadCertificate**: Uploads a system secure boot key through the BMC Redfish API, using `--file_type` and `--file`.
- **ResetAllKeysToDefault**: Resets all system secure boot keys to default through the BMC Redfish API.
- **DeleteAllKeys**: Deletes all system secure boot keys through the BMC Redfish API.
- **DeletePK**: Deletes the system secure boot PK through the BMC Redfish API.

## Options

- `--action <action>`: Sets action to 1 = Status, 2 = Enable, 3 = Disable, 4 = Showdatabases, 5 = UploadCertificate, 6 = ResetAllKeysToDefault, 7 = DeleteAllKeys, 8 = DeletePK.
- `--file_type <file type>` (Optional): Selects the type of secure boot key. Format includes "PK," "KEK," "db," "dbr," "dbt," or "dbx" (case sensitive). "dbx" can only be used with the ShowDatabases action.
- `--file` (Optional): Uploads the secure boot key in PEM format.
- `--individually` (Optional): Updates each system's secure boot keys individually with the corresponding secure boot key.
- `--reboot` (Optional): Forces the managed system to reboot or power up after operation.
- `--post_complete` (Optional): Waits for the managed system's POST to complete after reboot.

## Examples

### Enable
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureBootManage --redfish --action Enable
```

### UploadCertificate
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureBootManage --redfish --action UploadCertificate --file_type KEK --file CertificateFile.pem
```

### Showdatabases (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SecureBootManage --redfish --action ShowDatabases
```

### Status (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SecureBootManage --redfish --action Status
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l Slist.txt -u ADMIN -p PASSWORD -c SecureBootManage --redfish --action UploadCertificate --file_type PK --file CertificateFile.pem --individually --reboot --post_complete
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### Enable
```
Status: Secure boot is enabled for 192.168.34.56
Note: You have to reboot or power up the system for the BIOS changes to take
effect.
```

### UploadCertificate
```
Status: Certificate is uploaded for 192.168.34.56
Note: You have to reboot or power up the system for the BIOS changes to take
effect.
```

### Showdatabases
```
Managed system............................10.184.16.102
 Number of Platform Keys(PK)...........1
 Number of Key Exchange Keys(KEK)......0
 Number of Authorized Signatures(db)...0
 Number of OS Recovery Signatures(dbr).0
 Number of Authorized Timestamps(dbt)..0
 Number of Forbidden Signatures(dbx)...0
```

### Status
```
Managed system................192.168.34.57
 Secure boot status........Disabled
```

## Notes

- This command is only available on X13/H13 and later platforms, and requires the SFT-DCMS-SINGLE license.
- You have to reboot or power up the system for BIOS changes to take effect.
- The `--file_type` argument is "PK," "KEK," "db," "dbr," "dbt," or "dbx" (case sensitive). "dbx" can only be used with the ShowDatabases action.
- The `--file` option only supports PEM files.
- The default BIOS setting for secure boot mode is Custom, with no secure boot key, and secure boot is not enabled by default. Before enabling secure boot, either add a key or change the secure boot mode to Standard using the `ChangeBiosCfg` command.
