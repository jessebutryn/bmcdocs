# UpdateBios

Updates the BIOS firmware image on the managed system.

## Syntax

### OOB and In-Band
```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c UpdateBios --file <filename> [options…]
```

### Remote In-Band
```
sum [-I Remote_INB | -I Remote_RHI -u <username> -p <password>] --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c UpdateBios --file <filename> [--remote_sum <remote sum path>] [options…]
```

### Seamless Update (X13 RoT platform or later)
```
sum <-i <IP or host name> | -I Redfish_HI> -u <username> -p <password> -c UpdateBios --file <CAPSULE_FILE.bin> [--staged update] [--reboot] [--post_complete]
```

### Remote In-Band Seamless Update
```
sum -I Remote_RHI -u <username> -p <password> --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c UpdateBios --file <CAPSULE_FILE.bin> [--staged update] [--reboot] [--post_complete] [--remote_sum <remote sum path>]
```

## Options

- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--flash_smbios`: Overwrites and resets the SMBIOS data.
- `--preserve_mer`: Preserves the ME firmware region.
- `--preserve_nv`: Preserves the NVRAM.
- `--kcs`: Updates BIOS through KCS. (Support is available on platforms before X11 with OEM BMC request only and can be only used with in-band usage.)
- `--preserve_setting`: Preserves BIOS configurations.
- `--erase_OA_key`: Erases the OA key.
- `--backup`: Backs up the current BIOS image. (Only supported by RoT systems.)
- `--forward`: Confirms the Rollback ID and upgrades to the next revision. (Only supported by X12/H12 and later platforms except for H12 non-RoT systems.)
- `--staged <action>`: Sets action to:
  - `1 = update`: The Update process will start at the next system boot.
  - `2 = abort`: Aborts the previous staged update task.
  - `3 = getinfo`: Check if there was any pending staged update task.
- `--post_complete`: Waits for the managed system POST to complete after reboot.
- `--clear_password`: Clears the BIOS password.
- `--erase_secure_boot_key`: Erases the secure boot key.
- `--reset_boot_option`: Resets the BIOS boot configurations.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBios --file Supermicro_BIOS.rom --reboot
```

### In-Band
```
[SUM_HOME]# ./sum -c UpdateBios --file Supermicro_BIOS.rom --reboot
```

### In-Band through KCS
```
[SUM_HOME]# ./sum -c UpdateBios --file Supermicro_BIOS.rom --kcs --reboot
```

### In-Band through Redfish Host Interface
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateBios --file Supermicro_BIOS.rom --reboot
```

### Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c UpdateBios --file Supermicro_BIOS.rom --reboot --remote_sum /root/sum
```

### Remote In-Band through Redfish Host Interface
```
[SUM_HOME]# ./sum -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.56 --ou root --op 111111 -c UpdateBios --file Supermicro_BIOS.rom --reboot --remote_sum /root/sum
```

### Seamless Update OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBios --file CAPSULE_FILE.bin --reboot --post_complete
```

### Seamless Update In-Band
```
[SUM_HOME]# ./sum -I Redfish_HI -c UpdateBios --file CAPSULE_FILE.bin
```

### Seamless Update Remote In-Band
```
[SUM_HOME]# ./sum -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.56 --ou root --op 111111 -c UpdateBios --file CAPSULE_FILE.bin --remote_sum /root/sum
```

## Notes

- Before performing the OOB UpdateBios command, it is recommended to shut down the managed system first.
- When performing an in-band UpdateBios command, SUM will disable watchdog and unload the me/mei driver from the OS if it exists.
- With the Server ME embedded on the Supermicro system, you may encounter a problem executing the "UpdateBios" in-band SUM command when the Client ME driver (MEIx64) is installed on the Windows platform. To prevent the system from hanging, you need to remove the driver before updating BIOS. The steps are displayed upon detection.
- When using an SSH connection to run the UpdateBios in-band command, the SSH timeout on both the client and server sides should be adjusted to avoid a broken pipe during command execution. Typical execution time is within 30 minutes. Timeout value should be longer than 30 minutes.
- If the updated BIOS FDT (Flash Descriptor Table) is different from the current BIOS FDT or if ME protection needs to be disabled when the UpdateBios in-band command is executed, a warning message stating the necessary actions is displayed.
- When multiple boots are installed, use the default boot OS to run this command so that when FDT is different, the jumper-less solution can continue updating BIOS after the first reboot.
- OOB UpdateBios command has not been supported for MBs that implemented client ME such as X13SAx series, X12SAE, X12SCA-(5)F, X11SAE-F, X11SAT-F, X11SSZ-(Q)F/LN4F, X11SBA-(LN4)F and C7-series.
- Signed BIOS update is supported.
- X12/H12 RoT platforms support staged update only if both BMC and CPLD support it as well.
- For some X12/H12 RoT platforms, BIOS can only be updated while the system is powered off. In this case, the --reboot option is required. Therefore, for in-band BIOS updates, SUM will power off the system after uploading BIOS image to start the update process. The system will be powered on automatically after the BIOS update has completed.
- For X12/H12 and later RoT platforms, in-band BIOS updates can only be done through the Redfish Host Interface. For details, refer to 4.10 Redfish Host Interface.
- The --backup option backs up the current BIOS image on the managed system, not the BIOS file to be updated.
- The --backup option is only supported by X12/H12 and later RoT platforms.
- Due to a known GRUB2 loader issue, the system may not be able to boot and may hang up after BIOS update is upgraded. If the GRUB2 loader version is not the latest, please downgrade the BIOS to the previous version and upgrade the GRUB2 loader to the latest version. Then perform a BIOS upgrade to the target BIOS again. For more details, please refer to the FAQ on the Supermicro website https://www.supermicro.com/support/faqs/faq.cfm?faq=33400.
- OpenBMC only accepts tar firmware files for BIOS firmware updates. Please refer to the appendix L.1 BIOS Firmware Updating Tar File for OpenBMC for creating a tar file firmware image.
- The OOB usage of this function is available when the BMC node product key is activated.
- The in-band usage of this function does not require node product key activation.
- The firmware image can be successfully updated only when the board ID of the firmware image and the managed system are the same.
- You have to reboot or power up the managed system for the changes to take effect.
- When using an OOB channel, if the onboard BIOS or the BIOS firmware image does not support OOB functions, the DMI information (such as the motherboard serial number) might be lost after system reboot.
- DO NOT flash the BIOS and BMC firmware images at the same time.
- The --preserve_nv and --flash_smbios options cannot be used at the same time.
- The --flash_smbios option is used to erase and restore SMBIOS information as factory default values. Unless you are familiar with SMBIOS data, do not use this option.
- The --preserve_nv option is used to preserve BIOS NVRAM data. Unless you are familiar with BIOS NVRAM, do not use this option.
- The --preserve_mer option is used to preserve the ME firmware region. Unless you are familiar with the ME firmware region, do not use this option.
- The --preserve_setting option requires an SFT-OOB-LIC key (both OOB and In-Band), and it is only supported on X11 Intel® Xeon® Scalable Processors with Intel® C620 Series Chipsets and later platforms. The preserved setting configurations will be listed in a preserved_settings.log. Another way to know which BIOS setting is preserved is to run the GetCurrentBioscfg and GetDefaultBioscfg commands after BIOS is updated. Compare the two files and the different values between these two files are the preserved settings.
- Firmware verification to update the BMC is supported. SUM prevents the BMC from being updated with unauthorized firmware.
- In-band usage through KCS is only supported on non-Redfish platforms (before X11 platforms) with an OEM BMC request only. It is not generally supported on a standard BMC.
- Seamless Update feature only supported on X13 RoT platform or later.
- This command is only available on SUM 2.9.0 or later.
- Updating a capsule file employs the same command as updating a full BIOS file. There are certain rules to keep in mind while using this function:
  1. There is anti-rollback mechanism to prevent users from downgrading capsule files based on the package versions.
  2. If users see the "layout ID mismatch" error message, it means that users need to update the full BIOS image that has the same layout ID with the desired capsule to update into the motherboard.
  3. If users see the "Invalid Capsule file" error message, users need to get the correct capsule file designed for that specific platform type, such as: capsule designed for X13 can't be used on other platforms.
  4. Some options will be ignored when updating a capsule file, including --backup, --preserve_setting, --flash_smbios, --erase_OA_key, --clear_password, --erase_secure_boot_key, and --reset_boot_option.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/updatebios.md