# CheckOOBSupport

Checks if both BIOS and BMC firmware images support OOB (Out-Of-Band) functions.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c CheckOOBSupport
```

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckOOBSupport
```

### In-Band
```bash
[SUM_HOME]# ./sum -c CheckOOBSupport
```

## Output

The console output contains information about:

- Node Product Key Format
- Node Product Key Activated status
- Feature Toggled On status
- BMC firmware version
- BMC OOB support status
- BIOS build date
- BIOS OOB support status
- RoT features support status

Example output:
```
[KEY]
Node Product Key Format..........JSON
Node Product Key Activated.......OOB
 SFT-DCMS-SVC-KEY Activated...Yes
 SFT-SDDC-SINGLE Activated....Yes
Feature Toggled On...............YES
[BMC]
BMC FW Version...................02.41
BMC Supports OOB BIOS Config.....Yes
BMC Build Date...................2022/05/27
[BMC ROT]
BMC Supports RoT.................Yes
[BMC ROT SIGNED]
BMC RoT Signed...................Yes
[BIOS]
BIOS Build Date..................2022/05/27
BIOS Supports OOB................Yes
[BIOS ROT]
BIOS Supports RoT................Yes
[BIOS ROT SIGNED]
BIOS RoT Signed..................Yes
```

## Notes

- If BMC does not support OOB, update BMC firmware using UpdateBmc command
- If BIOS does not support OOB, use UpdateBios command (OOB or in-band)
- When using OOB and BIOS doesn't support OOB, DMI info may be lost after reboot
- If Feature Toggled On is "No", all licensed features are disabled
- Known limitation: Rollback from OOB-supported to non-supported BIOS doesn't update build date and OOB support fields
