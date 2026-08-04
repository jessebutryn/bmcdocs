# UpdateBios

Updates the BIOS on the managed system with the given BIOS firmware image file (`Supermicro_BIOS.bin`, or `bios_image.tar` for OpenBMC).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateBios --file <filename> [options...]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c UpdateBios --file <filename> [options...]
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c UpdateBios --file <filename> [--remote_saa <remote SAA path>] [options...]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateBios --file <filename> [options...]
```

### Multiple Systems Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI} -l <system list file> -c UpdateBios --file <filename> [--remote_saa <remote SAA path>] [options...]
```

## Options

- `--reboot`: Forces the managed system to reboot or power up after operation
- `--individually`: Individually updates each BIOS with its corresponding image file
- `--flash_smbios`: Overwrites and resets the SMBIOS data. Used only for specific purposes; unless you are familiar with SMBIOS data, do not use this option
- `--preserve_nv`: Preserves the NVRAM. Used only for specific purposes; unless you are familiar with BIOS NVRAM, do not use this option (not available on X12 and later systems)
- `--preserve_mer`: Preserves the ME firmware region. Used only for specific purposes; unless you are familiar with the ME firmware image, do not use this option (not available on X12 and later RoT systems)
- `--preserve_setting`: Preserves BIOS configurations. Used only for specific purposes; unless you are familiar with BIOS configurations, do not use this option
- `--erase_OA_key`: Erases OA key
- `--backup`: Backs up the current BIOS image (only supported by RoT systems)
- `--forward`: Confirms the Rollback ID and upgrades to the next revision
- `--staged <action>`: Sets action to `1` = update (update process starts at next system boot), `2` = abort (aborts previously staged update task), `3` = getinfo (checks whether a staged update task is pending)
- `--post_complete`: Waits for the managed system's POST to complete after reboot
- `--clear_password`: Clears BIOS password
- `--erase_secure_boot_key`: Erases secure boot key
- `--reset_boot_option`: Resets BIOS boot configurations
- `--restore_optimized_default`: Restores the BIOS configurations to optimized default settings
- `--redfish`: Enables support for pure Redfish
- `--upgrade_only`: Firmware updates are only performed when the version is newer
- `--check_reboot_required`: Displays a warning message when a system reboot or power cycle is required
- `--remote_saa <remote SAA path>`: Path to remote SAA executable (for remote in-band)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBios --file Supermicro_BIOS.bin --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -c UpdateBios --file Supermicro_BIOS.bin --reboot
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateBios --file Supermicro_BIOS.bin --reboot
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c UpdateBios --file Supermicro_BIOS.bin --reboot --remote_saa /root/saa
```

### Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.56 --ou root --op 111111 -c UpdateBios --file Supermicro_BIOS.bin --reboot --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateBios --file Supermicro_BIOS.bin
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c UpdateBios --file Supermicro_BIOS.bin
```

### Seamless Update capsule file (X13 RoT or later)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBios --file CAPSULE_FILE.bin --reboot --post_complete
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateBios --file CAPSULE_FILE.bin --reboot
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.56 --ou root --op 111111 -c UpdateBios --file CAPSULE_FILE.bin --remote_saa /root/saa
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateBios --file CAPSULE_FILE.bin --reboot --post_complete
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c UpdateBios --file CAPSULE_FILE.bin --reboot --post_complete
```

## Notes

- BIOS secure flash and RoT signed information are supported.
- Before performing the OOB `UpdateBios` command, it is recommended to shut down the managed system first.
- When performing an in-band `UpdateBios` command, SAA disables the watchdog and unloads the me/mei driver from the OS if it exists. If the Client ME driver (MEIx64) is installed on Windows, remove it first to avoid the system hanging; steps are displayed upon detection.
- When using SSH to run the in-band `UpdateBios` command, adjust SSH timeouts on both client and server to avoid a broken pipe; typical execution time is within 30 minutes, so the timeout should be longer than 30 minutes.
- If the updated BIOS FDT differs from the current BIOS FDT, or ME protection needs to be disabled, a warning message with necessary actions is displayed.
- When multiple boots are installed, use the default boot OS to run this command so the jumper-less solution can continue after the first reboot if FDT differs.
- OOB `UpdateBios` is not supported for motherboards implementing client ME, such as X13SAx series, X12SAE, and X12SCA-(5)F.
- X12/H12 RoT platforms support staged update only if both BMC and CPLD also support it.
- For some X12/H12 RoT platforms, BIOS can only be updated while the system is powered off, requiring `--reboot`. For in-band updates, SAA powers off the system after uploading the image and powers it back on automatically after completion.
- For X12/H12 and later RoT platforms, in-band BIOS updates can only be done through the Redfish Host Interface.
- The `--backup` option backs up the current BIOS image on the managed system, not the file being updated.
- Due to a known GRUB2 loader issue, the system may hang after a BIOS update; downgrade BIOS, upgrade GRUB2, then upgrade BIOS again if needed.
- OpenBMC only accepts tar firmware files for BIOS firmware updates.
- The OOB usage of this function requires the BMC node product key to be activated; in-band usage does not.
- The firmware image can only be updated when the board ID of the image matches the managed system.
- You must reboot or power up the managed system for changes to take effect.
- Over OOB, if the onboard BIOS or firmware image does not support OOB functions, DMI information (such as motherboard serial number) might be lost after reboot.
- Do not flash the BIOS and BMC firmware images at the same time.
- `--preserve_nv` and `--flash_smbios` cannot be used at the same time.
- `--preserve_setting` requires an SFT-OOB-LIC key (both OOB and in-band) for X12 3rd Gen Intel Xeon Scalable processors with Intel C620 Series Chipsets. Preserved settings are listed in `preserved_settings.log`; alternatively, compare `GetCurrentBiosCfg` and `GetDefaultBiosCfg` output after the update to identify preserved settings.
- Firmware verification is supported to prevent updating the BMC with unauthorized firmware.
- When updating a capsule file, an anti-rollback mechanism prevents downgrading based on package versions. A "layout ID mismatch" error means the full BIOS image with a matching layout ID must be updated first. An "Invalid Capsule file" error means the capsule file is not designed for that platform (e.g. an X13 capsule cannot be used on other platforms).
- Some options are ignored when updating a capsule file: `--backup`, `--preserve_setting`, `--flash_smbios`, `--erase_OA_key`, `--clear_password`, `--erase_secure_boot_key`, and `--reset_boot_option`.
