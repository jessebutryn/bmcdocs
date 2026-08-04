# GetTpmInfo

Gets the TPM (Trusted Platform Module) information from the managed system. SAA has two implementations for OTA TPM management: Intel OTA and Supermicro OTA; the supported OTA solution can be determined from this command's output.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetTpmInfo [--showall] [--current_password <current password> | --cur_pw_file <current password file path>]
```

### In-Band
```
saa -c GetTpmInfo [--showall] [--current_password <current password> | --cur_pw_file <current password file path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetTpmInfo [--showall] [--current_password <current password> | --cur_pw_file <current password file path>]
```

## Options

- `--current_password <current password>` (Optional): Checks the current BIOS Administrator password.
- `--showall` (Optional): Prints the NV data and the capability flags (if applicable) of the trusted platform module. Only supported for Intel platforms; only the Supermicro OTA solution supports this option.
- `--cur_pw_file <Current password file>` (Optional): The specified file path to read the current password.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetTpmInfo --showall
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetTpmInfo --showall
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetTpmInfo --showall
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### TPM 1.2 with --showall (Query through Supermicro OTA)
```
TPM Information
================
 TXT Support: Yes
 TPM Support: dTPM supported
 TXT Status: Disabled
 dTPM Status: Enabled
 fTPM Status: Disabled
 TPM Version: TPM 1.2
 TPM Provisioned: Yes
 TPM Ownership: No
 TPM PS NV Index write-protected: No
 TPM AUX NV Index write-protected: No
 TPM PO NV Index write-protected: No
 TPM Locked: Yes
TPM 1.2 PS NV index LCP Definition
===================================
 [NV Public Data]
 Tag: 0x0018
 NV index: 0x50000001
 ...
TPM 1.2 Capability Flags
========================
 [Volatile Flags]
 deactivated: 0
 disableForceClear: 0
 physicalPresence: 0
 physicalPresenceLock: 1
 bGlobalLock: 0
 [Permanent Flags]
 disable: 0
 ownership: 1
 deactivated: 0
 readPubEK: 1
 disableOwnerClear: 0
 allowMaintenance: 0
 physicalPresenceLifetimeLock: 0
 physicalPresenceHWEnable: 0
 physicalPresenceCMDEnable: 1
 FIPS: 0
 enableRevokeEK: 0
 nvLocked: 1
 tpmEstablished: 0
```

### TPM 2.0 with --showall (Query through Supermicro OTA)
```
TPM Information
================
 TXT Support: Yes
 TPM Support: dTPM supported
 TXT Status: Enabled
 dTPM Status: Enabled
 fTPM Status: Disabled
 TPM Version: TPM 2.0
 TPM Provisioned: Yes
 TPM Ownership: No
 TPM PS NV Index write-protected: No
 TPM AUX NV Index write-protected: No
 TPM PO NV Index write-protected: No
TPM 2.0 PS NV index LCP Definition
==========================
 [NV Public Data]
 NvIndex: 0x01C10103
 NameAlg: SHA256
 Attributes: 0x62040408
 ...
```

## Notes

- This command will query the TPM module information through Intel OTA or Supermicro OTA.
- The "TPM Locked" field in the TPM Information section is only for TPM 1.2.
- The "Capability Flags" section is only for TPM 1.2.
- The `--showall` option is optional. The "PS NV INDEX LCP Definition," "AUX NV INDEX LCP Definition," "PPI NV INDEX LCP Definition," and "Capability Flags" sections are only displayed when `--showall` is assigned.
- `TpmManage` is not supported on AMD platforms.
- If the execution "Status" field for a managed system is SUCCESS, the TPM module information of the managed system will be shown in the Execution Message section of the created log file.
