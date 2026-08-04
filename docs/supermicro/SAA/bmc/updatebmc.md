# UpdateBmc

Updates the BMC with the given BMC firmware image file (`Supermicro_BMC.bin`, or `bmc_image.tar` for OpenBMC).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateBmc --file <filename> [--overwrite_cfg] [--overwrite_sdr] [--backup] [--forward] [--overwrite_ssl]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c UpdateBmc --file <filename> [--overwrite_cfg] [--overwrite_sdr] [--backup] [--forward] [--overwrite_ssl]
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c UpdateBmc --file <filename> [--overwrite_cfg] [--overwrite_sdr] [--backup] [--forward] [--overwrite_ssl] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateBmc --file <filename> [--overwrite_cfg] [--overwrite_sdr] [--backup] [--forward] [--overwrite_ssl]
```

## Options

- `--file <file name>`: Required. Updates the BMC with the given BMC file
- `--individually`: Updates each BMC with its corresponding image file individually
- `--overwrite_cfg`: Overwrites the current BMC configuration using the factory default values in the given BMC image file
- `--overwrite_sdr`: Overwrites current BMC SDR data (for AMI BMC FW, must also use `--overwrite_cfg`)
- `--overwrite_ssl`: Overwrites current BMC SSL configuration
- `--backup`: Backs up the current BMC image (only supported by RoT systems)
- `--forward`: Confirms the Rollback ID and upgrades to the next revision
- `--bmc_boot_check`: Checks if BMC boots up within 16 minutes after update (only supported on X12/H12 and later platforms except H12 non-RoT systems)
- `--redfish`: Enables support for pure Redfish
- `--upgrade_only`: Firmware updates are only performed when the version is newer
- `--check_reboot_required`: Displays a warning message when a system reboot or power cycle is required

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBmc --file Supermicro_BMC.bin
```

### In-Band
```bash
[SAA_HOME]# ./saa -c UpdateBmc --file Supermicro_BMC.bin
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateBmc --file Supermicro_BMC.bin
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c UpdateBmc --file Supermicro_BMC.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateBmc --file Supermicro_BMC.bin
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c UpdateBmc --file Supermicro_BMC.bin
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c UpdateBmc --file Supermicro_BMC.bin
```

## Output

```
Managed system...........192.168.34.56
 BMC UFFN.............BMC_X13AST2600-ROT20-D301MS_20240418_01.02.31_STDsp.bin
 BMC type.............X13_RoT2.0_ATEN_AST2600_2_1
 BMC version..........01.02.31
 BMC build date.......2024/04/18
Local BMC image file.....BMC_X13AST2600-ROT20-D301MS_20240418_01.02.31_STDsp.bin
 BMC UFFN.............BMC_X13AST2600-ROT20-D301MS_20240418_01.02.31_STDsp.bin
 BMC type.............X13_RoT2.0_ATEN_AST2600_2_1
 BMC version..........01.02.31
 BMC build date.......2024/04/18
 FW image.............Signed
 Signed Key.......RoT
Status: Start updating BMC for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW...........................Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: BMC is updated for 192.168.34.56
Update Complete. Please wait for BMC reboot, about 4 mins.
..................................................
..................................................
..................................................
..................................................
....................................Done
```

## Notes

- The BMC will be reset after updating.
- BMC configurations are preserved by default after updating unless the `--overwrite_cfg` option is used.
- Do not flash BIOS and BMC firmware images at the same time.
- The `--overwrite_sdr` option overwrites current BMC SDR data; for AMI BMC FW, it also requires `--overwrite_cfg`.
- Signed BMC update is supported.
- For X12/H12 and later platforms (except H12 non-RoT systems), in-band BMC update can only be done through the Redfish Host Interface.
- The `--backup` option backs up the current BMC image on the managed system, not the BMC file being updated to it, and is only supported by X12/H12 and later RoT platforms.
- The `--skip_unknown` option is designed to skip all invalid tables and settings in the latest BMC configuration in the managed system.
- To update BMC firmware while preserving settings: (1) run `UpdateBmc` without `--overwrite_cfg` (settings are preserved by default), (2) dump the new BMC configuration with `GetBmcCfg`, (3) modify the configuration file as needed (e.g. change `<LanInterface>` from "Failover" to "Dedicated" in the `<LAN>` table), (4) apply it with `ChangeBmcCfg`.
- The execution progress for the managed system is continuously updated to the "Execution Message" section of the managed system in the created log file.
