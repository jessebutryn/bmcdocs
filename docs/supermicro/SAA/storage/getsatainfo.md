# GetSataInfo

Gets the current SATA HDD information under the on-board AHCI controller from the managed system. OOB only.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSataInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSataInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSataInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSataInfo
```

## Output

```
SATA HDD Information
====================
 [HDD(0)]
 Controller Name: PCH SATA
 Configuration Type: AHCI
 Slot ID: 0
 Slot Populated: Yes
 Model Name: INTEL SSDSC2BB120G4
 Serial Number: PHWL542502J2120LGN
 HDD Firmware Version: D201037
 S.M.A.R.T. Supported: Yes
```

## Notes

- If the execution Status field of the managed system shows SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
