# TpmManage

Enables and clears TPM module capabilities, and provisions the TPM module, on X11 Intel Xeon Scalable Processors with Intel C620 Series Chipsets and later platforms. Before executing the command, the TPM module should be installed on the managed system. Not supported on AMD platforms.

## Syntax

### Provisioning (OOB)
```
saa -i <IP or host name> -u <username> -p <password> -c TpmManage --provision [options...]
```

### Provisioning (In-Band)
```
saa -c TpmManage --provision [options...]
```

### Provisioning (Multiple Systems OOB)
```
saa -l <system list file> [-u <username> -p <password>] -c TpmManage [options...]
```

### Enabling/Clearing (OOB)
```
saa -i <IP or host name> -u <username> -p <password> -c TpmManage {options...} [--reboot]
```

### Enabling/Clearing (In-Band)
```
saa -c TpmManage {options...} [--reboot]
```

### Enabling/Clearing (Multiple Systems OOB)
```
saa -l <system list file> [-u <username> -p <password>] -c TpmManage {options...} [--reboot]
```

## Options

- `--reboot` (Optional): Forces the managed system to reboot or power up after operation.
- `--clear_and_enable_dtpm_txt` (Optional): Clears dTPM ownership and activates dTPM/TXT.
- `--clear_dtpm` (Optional): Clears dTPM ownership and disables dTPM for TPM 1.2. Clears dTPM ownership for TPM 2.0.
- `--enable_txt_and_dtpm` (Optional): Enables TXT and dTPM.
- `--clear_and_enable_dtpm` (Optional): Clears dTPM ownership, disables dTPM (for TPM 1.2 only), and activates dTPM.
- `--disable_dtpm` (Optional): Disables dTPM.
- `--disable_txt` (Optional): Disables TXT.
- `--provision` (Optional): Launches the trusted platform module provision procedure.
- `--table_default` (Optional): Uses the default TPM provision table.
- `--table <table name>` (Optional): Uses the given customized TPM provision table file.
- `--post_complete` (Optional): Waits for the managed system's POST to complete after rebooting.

## Examples

### Provisioning with Default Table
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --provision --table_default --reboot
[SAA_HOME]# ./saa -c TpmManage --provision --table_default --reboot
```

### Provisioning with Custom Table
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --provision --table Tpm12Prov.bin --reboot
[SAA_HOME]# ./saa -c TpmManage --provision --table Tpm12Prov.bin --reboot
```

### Multiple Systems OOB Provisioning
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --provision --table_default --reboot
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c TpmManage --provision --table Tpm12Prov.bin --reboot
```

### Clear and Enable dTPM/TXT
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --clear_and_enable_dtpm_txt --reboot
[SAA_HOME]# ./saa -c TpmManage --clear_and_enable_dtpm_txt --reboot
```

### Clear dTPM
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --clear_dtpm --reboot
[SAA_HOME]# ./saa -c TpmManage --clear_dtpm --reboot
```

### Enable TXT and dTPM
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --enable_txt_and_dtpm --reboot
[SAA_HOME]# ./saa -c TpmManage --enable_txt_and_dtpm --reboot
```

### Clear and Enable dTPM
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --clear_and_enable_dtpm --reboot
[SAA_HOME]# ./saa -c TpmManage --clear_and_enable_dtpm --reboot
```

### Disable dTPM
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --disable_dtpm --reboot
[SAA_HOME]# ./saa -c TpmManage --disable_dtpm --reboot
```

### Disable TXT
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c TpmManage --disable_txt --reboot
[SAA_HOME]# ./saa -c TpmManage --disable_txt --reboot
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

If the execution "Status" field for a managed system is SUCCESS, the TPM provisioning procedure is completed.

## Notes

- This command is supported on X11 Intel Xeon Scalable Processors with Intel C620 Series Chipsets or later platforms.
- The system may reboot several times during provisioning.
- Execute the `GetTpmInfo` command to obtain the OTA supported type before doing TPM provision.
- The TPM module will be locked when the provisioning procedure is completed.
- Using `--table_default` executes TPM provisioning with the default TPM provision table created by BIOS. Using `--table` executes TPM provisioning with a customized TPM provision table created by the user.
- The `--reboot` option is required by the TPM provision procedure for OOB Intel OTA solutions.
- When using TPM provision with in-band Intel OTA, follow these steps: (1) run `TpmManage --clear_and_enable_dtpm --reboot` to enable TPM; (2) run `TpmManage --provision` and then reboot the managed system manually; (3) run `TpmManage --enable_txt_and_dtpm --reboot` to enable TPM and TXT.
- The `--clear_and_enable_dtpm_txt` and `--enable_txt_and_dtpm` options cannot be used when TPM is not provisioned.
- The `--disable_dtpm` option cannot be used when TXT is enabled, and is not supported from the 14th generation Intel platform.
- The `--reboot` option is optional for in-band usage. Without it, the managed system will not reboot, and SAA will remind the user to reboot manually.
- The options of each use case are mutually exclusive.
