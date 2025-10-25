# GetTpmInfo

## Description

Use the "GetTpmInfo" command to get the TPM module information from the managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c GetTpmInfo [--showall]
```

## Options

- `--showall`: Shows all TPM information (only supported by Supermicro OTA).

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetTpmInfo --showall
```

### In-Band
```
[SUM_HOME]# ./sum -c GetTpmInfo --showall
```

The console output contains the following information when installing the TPM 1.2 module.

```
Supermicro Update Manager (for UEFI BIOS) 2.1.0 (2018/02/09) (x86_64)
Copyright(C)2018 Super Micro Computer, Inc. All rights reserved.
Query through Supermicro OTA
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
```

The following information is displayed only when the command “GetTpmInfo” is executed with the option “--showall”. Only the Supermicro OTA solution supports the option “--showall”.

```
TPM 1.2 PS NV index LCP Definition
===================================
 [NV Public Data]
 Tag: 0x0018
 NV index: 0x50000001
 ReadSizeOfSelect: 0x0003
 ReadPCRSelect[0]: 0x00
 ReadPCRSelect[1]: 0x00
```
