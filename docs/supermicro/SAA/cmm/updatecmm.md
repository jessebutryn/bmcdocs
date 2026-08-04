# UpdateCmm

Updates the CMM firmware image on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateCmm --file <filename> [--overwrite_cfg] [--overwrite_sdr] [--overwrite_ssl] [--cmm_boot_check]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateCmm --file <filename> [--overwrite_cfg] [--overwrite_sdr] [--overwrite_ssl] [--cmm_boot_check]
```

## Options

- `--file <file name>`: Updates the CMM with the given image file.
- `--individually`: Updates each CMM with its corresponding image file individually (optional).
- `--overwrite_cfg`: Overwrites the current CMM configurations, including network settings, using the factory default values in the given CMM image file. This might cause the IPMI connection to be lost (optional).
- `--overwrite_sdr`: Overwrites the current CMM SDR data. Only supported by the CSE-947HE2C-R2K05JBOD system (optional).
- `--overwrite_ssl`: Overwrites the current CMM SSL configuration. Only supported by the CSE-947HE2C-R2K05JBOD system (optional).
- `--backup`: Backs up the current CMM image. Only supported by RoT systems (optional).
- `--cmm_boot_check`: Checks if the CMM has booted up after a reset (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateCmm --file Supermicro.CMM.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateCmm --file Supermicro.CMM.bin
```

## Notes

- CMM will be reset after updating.
- CMM configurations are preserved after updating unless the `--overwrite_cfg` option is used.
- Do not flash BIOS and BMC firmware images at the same time.
- The `--overwrite_cfg` option overwrites the current CMM configurations, including network settings, with the factory default values in the given CMM firmware image. This might cause the IPMI connection to be lost.
- The `--overwrite_sdr` and `--overwrite_ssl` options currently only take effect on the JBOD CMM system CSE-947HE2C-R2K05JBOD; other CMM systems ignore them.
- If the CMM FW web server becomes unreachable after the CMM FW is updated, use ipmitool to troubleshoot: reset the CMM, wait three minutes and check if the CMM web is reachable; if still unreachable, load the CMM factory defaults (all CMM settings except LAN/FRU will be lost), then wait three minutes and check again.
- Use the UpdateCmm command to update the CSE-946ED-R2KJBOD and CSE-947HE2C-R2K05JBOD JBOD systems.
- The execution progress is continuously updated in the Execution Message section of the created log file.
