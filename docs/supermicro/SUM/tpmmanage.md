# TpmManage

Manages TPM (Trusted Platform Module) capabilities on the managed system.

## Syntax

### Provisioning TPM Module (X11 and later platforms)
```
sum [-i <IP or host name> -u <username> -p <password>] -c TpmManage --provision [options…]
```

### Enabling and Clearing TPM Module Capabilities (X11 and later platforms)
```
sum [-i <IP or host name> -u <username> -p <password>] -c TpmManage [options…] [--reboot]
```

### OpenBMC Provisioning
```
sum -l <system list file> [-u <username> -p <password>] -c TpmManage --provision [options…]
```

### OpenBMC Enabling and Clearing
```
sum -l <system list file> [-u <username> -p <password>] -c TpmManage [options…] [--reboot]
```

## Options

### Provisioning Options
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--provision`: Launches the trusted platform module provision procedure.
- `--table_default`: Uses the default TPM provision table.
- `--table <file name>`: Uses the customized TPM provision table.

### Management Options
- `--reboot`: Forces the managed system to reboot.
- `--clear_and_enable_dtpm_txt`: Clears dTPM ownership and activates dTPM/TXT.
- `--clear_dtpm`: Clears dTPM ownership and disables dTPM for TPM 1.2. Clears dTPM ownership for TPM 2.0.
- `--enable_txt_and_dtpm`: Enables TXT and dTPM.
- `--clear_and_enable_dtpm`: Clears dTPM ownership, disables dTPM (for TPM 1.2 only) and activates dTPM.
- `--disable_dtpm`: Disables dTPM.
- `--disable_txt`: Disables TXT.

## Examples

### Provisioning with Default Table (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --provision --table_default --reboot
```

### Provisioning with Custom Table (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --provision --table Tpm12Prov.bin --reboot
```

### Provisioning with Default Table (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --provision --table_default --reboot
```

### Provisioning with Custom Table (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --provision --table Tpm12Prov.bin --reboot
```

### Clear and Enable dTPM/TXT (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --clear_and_enable_dtpm_txt --reboot
```

### Clear dTPM (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --clear_dtpm --reboot
```

### Enable TXT and dTPM (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --enable_txt_and_dtpm --reboot
```

### Clear and Enable dTPM (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --clear_and_enable_dtpm --reboot
```

### Disable dTPM (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --disable_dtpm --reboot
```

### Disable TXT (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --disable_txt --reboot
```

### Clear and Enable dTPM/TXT (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --clear_and_enable_dtpm_txt --reboot
```

### Clear dTPM (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --clear_dtpm --reboot
```

### Enable TXT and dTPM (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --enable_txt_and_dtpm --reboot
```

### Clear and Enable dTPM (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --clear_and_enable_dtpm --reboot
```

### Disable dTPM (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --disable_dtpm --reboot
```

### Disable TXT (In-Band)
```
[SUM_HOME]# ./sum -c TpmManage --disable_txt --reboot
```

### OpenBMC Provisioning with Default Table
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --provision --table_default --reboot
```

### OpenBMC Provisioning with Custom Table
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --provision --table Tpm12Prov.bin --reboot
```

### OpenBMC Clear and Enable dTPM/TXT
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --clear_and_enable_dtpm_txt --reboot
```

### OpenBMC Clear dTPM
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --clear_dtpm --reboot
```

### OpenBMC Enable TXT and dTPM
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --enable_txt_and_dtpm --reboot
```

### OpenBMC Clear and Enable dTPM
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --clear_and_enable_dtpm --reboot
```

### OpenBMC Disable dTPM
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --disable_dtpm --reboot
```

### OpenBMC Disable TXT
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --disable_txt --reboot
```

## Notes

- This command is supported on X11 Intel® Xeon® Scalable Processors with Intel® C620 Series Chipsets or later platforms.
- Before executing the command, the TPM module should be installed on the managed system.
- The system may be rebooted several times during provisioning.
- Please execute the GetTpmInfo command to obtain OTA supported type before doing TPM provision.
- The TPM module will have been locked when the provisioning procedure is completed.
- Executing the TpmManage command with the --table_default option will execute TPM provisioning with the default TPM provision table created by BIOS.
- Executing the TpmManage command with the --table option will execute TPM provisioning with customized TPM provision table created by user.
- The --reboot option is required by the TPM provision procedure for OOB Intel OTA solutions.
- For TPM provision use with in-band Intel OTA, please follow these steps to complete TPM provision:
  1. Execute the "TpmManage" command with the "--clear_and_enable_dtpm" and "--reboot" options to enable TPM.
  2. Execute the "TpmManage" command with the "--provision" option to do TPM provision and then reboot the managed system manually.
  3. Execute the "TpmManage" command with the "--enable_txt_and_dtpm" and "--reboot" options to enable TPM and TXT.
- The "--clear_and_enable_dtpm_txt" and "--enable_txt_and_dtpm" options cannot be used when TPM is not provisioned.
- The "--disable_dtpm" option cannot be used when TXT is enabled.
- Please execute the "GetTpmInfo" command to obtain the OTA supported type before using TPM.
- The "--reboot" option is optional for in-band usage. If executing a command without this option, the managed system will not reboot. Then SUM will remind the user to reboot the managed system manually.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/tpmmanage.md