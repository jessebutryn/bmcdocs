# CheckOOBSupport

Checks if both BIOS and BMC firmware images support OOB (Out-Of-Band) functions on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CheckOOBSupport
```

### In-Band
```
saa -c CheckOOBSupport
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CheckOOBSupport
```

## Options

None

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckOOBSupport
```

### In-Band
```bash
[SAA_HOME]# ./saa -c CheckOOBSupport
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CheckOOBSupport
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

If the execution "Status" field for a managed system is SUCCESS, the BIOS and BMC capabilities of the managed system are shown in the "Execution Message" section in the created log file.

```
[KEY]
Node Product Key Format..........JSON
Node Product Key Activated.......SFT-DCMS-SINGLE
 SFT-DCMS-SVC-KEY Activated...No
 SFT-SDDC-SINGLE Activated....No
Feature Toggled On...............Yes
[BMC]
BMC FW Version...................01.02.18
IPMI Version.....................2.0
Manufacturer ID..................7C 2A 00
Product ID.......................52 1C 00
Auxiliary Firmware Revision......18 01 00 00
BMC Supports OOB BIOS Config.....Yes
BMC Supports OOB DMI Edit........Yes
[BIOS]
Board ID.........................1C52
BIOS Build Date..................2023/10/19
BIOS Version.....................2.0
BIOS Supports OOB BIOS Config....Yes
BIOS Supports OOB DMI Edit.......Yes
```

## Notes

- If the BMC does not support OOB functions, update the BMC firmware image using the SAA `UpdateBmc` command.
- If the BIOS does not support OOB functions, use the SAA `UpdateBios` command (either in-band or OOB) to flash the BIOS even when it does not yet support OOB.
- When using the OOB channel, if the onboard BIOS or BIOS firmware image does not support OOB functions, DMI information (such as the motherboard serial number) might be lost after a system reboot.
- If Feature Toggled On is No, all licensed features are turned off and Node Product Key Activated is N/A.
- Known limitation: rolling back BIOS from an OOB-supported version to a non-supported version does not update the BIOS build date and OOB support fields accordingly.
