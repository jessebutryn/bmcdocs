# SecureEraseDisk

Securely erases an HDD on the managed system. After a secure erase is complete, the HDD is formatted and its password is cleared. An HDD without a password installed can be securely erased directly without a password or PSID. This command can also install an HDD password if no password is installed. SAA supports secure-erase in three security modes: TCG, SAT3, and Not TCG/SAT3 Supported.

## Syntax

### OOB (Pre-check)
```
saa -i <IP or host name> -u <username> -p <password> -c SecureEraseDisk [--current_password <current password> | --cur_pw_file <current password file path>] --file <filename> --precheck
```

### OOB (Action)
```
saa -i <IP or host name> -u <username> -p <password> -c SecureEraseDisk [--current_password <current password> | --cur_pw_file <current password file path>] --file <filename> --action <action> [--reboot [--post_complete]]
```

### In-Band
```
saa -c SecureEraseDisk [--current_password <current password> | --cur_pw_file <current password file path>] --file <filename> --precheck
saa -c SecureEraseDisk [--current_password <current password> | --cur_pw_file <current password file path>] --file <filename> --action <action> [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SecureEraseDisk [--current_password <current password> | --cur_pw_file <current password file path>] --file <filename> --precheck
saa -l <system list file> [-u <username> -p <password>] -c SecureEraseDisk [--current_password <current password> | --cur_pw_file <current password file path>] --file <filename> --action <action> [--reboot [--post_complete]]
```

## Actions

Supported actions vary by HDD security mode:

- **SetPassword**: Sets up an HDD password. (TCG, SAT3)
- **ChangePassword**: Changes the HDD password. Requires `new_password` in the input file. (TCG, SAT3)
- **ClearPassword**: Clears the HDD password. (TCG, SAT3)
- **SecurityErase**: Erases a device without an HDD password installed. If a password is installed, the device cannot be erased this way. (TCG, SAT3, Not TCG/SAT3 Supported)
- **SecurityErasePWD**: Erases a device with an HDD password. On SAT3, the password must be installed before erase. (TCG, SAT3)
- **SecurityErasePSID**: Erases a device with a PSID. (TCG only)

## Options

- `--current_password <current password>` (Optional): Checks the current BIOS Administrator password.
- `--cur_pw_file <Current Password File>` (Optional): The specified file path to read the current password.
- `--file <file name>`: HDD serial number mapping file. `PSID.txt` uses `serial number;PSID` format (TCG devices only); `Password.txt` uses `serial number;password;new_password` format (`new_password` required only for ChangePassword).
- `--reboot` (Optional): Forces the managed system to reboot or power up after operation.
- `--precheck` (Optional): Only displays HDD status (password status, security mode, TCG device type, and applicable actions).
- `--action <action>` (Optional): Sets secure erase action to 1 = SetPassword, 2 = SecurityErase, 3 = SecurityErasePWD, 4 = SecurityErasePSID, 5 = ChangePassword, 6 = ClearPassword.
- `--post_complete` (Optional): Waits for the managed system's POST to complete after reboot.

## Examples

### Pre-check
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseDisk --file Password.txt --precheck
[SAA_HOME]# ./saa -c SecureEraseDisk --file PSID.txt --precheck
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SecureEraseDisk --file psid.txt --precheck
```

### SetPassword
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseDisk --file Password.txt --action SetPassword --reboot
```

### SecurityErase
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseDisk --file Password.txt --action SecurityErase --reboot
```

### SecurityErasePWD (In-Band)
```bash
[SAA_HOME]# ./saa -c SecureEraseDisk --file Password.txt --action SecurityErasePWD --reboot
```

### SecurityErasePSID (In-Band)
```bash
[SAA_HOME]# ./saa -c SecureEraseDisk --file PSID.txt --action SecurityErasePSID --reboot
```

### With --post_complete
```bash
[SAA_HOME]# ./saa -i IP -u ADMIN -p PASSWORD -c SecureEraseDisk --file PSID.txt --action SecurityErasePSID --reboot --post_complete
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SecureEraseDisk --file psid.txt --action SetPassword --reboot
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### --precheck
```
Managed system............192.168.34.56
[HDD]
 Serial Number ..................S45RNE0M600194
 Password Status ................NOT INSTALLED
 Security Mode ..................SAT3 Supported
 Applicable Action...............SetPassword
 ...............SecurityErase
[HDD]
 Serial Number..................W472TJXH
 Password Status................INSTALLED
 Security Mode..................TCG Supported
 TCG Device Type................TCG-Enterprise
 Applicable Action..............SecurityErasePWD
 ..............SecurityErasePSID
 ..............ChangePassword
 ..............ClearPassword
Estimated security erase time......33 Minutes
Please check PreCheckFile for the mismatched HDDs.
```

### Action with --post_complete
```
Status: Enable Secure Erase Automation.
Status: The managed system 192.168.34.56 is rebooting.
.............................................
..................................................
..........................................Done
........
..................................................
.....................
Status: Security erase for HDD is set for 192.168.34.56
Status: The managed system 192.168.34.56 is waiting for POST complete
Status: PCIResourceConfigStarted
............................
................
Status: MemoryInitializationStarted
........................
Status: PCIResourceConfigStarted
..........
.....................
Status: MemoryInitializationStarted
......................
Status: MemoryInitializationStarted
.......
..............
Status: PCIResourceConfigStarted
..................
Status: The managed system 192.168.34.56 is POST completed
```

### Action without --post_complete
```
Status: Enable Secure Erase Automation.
Status: The managed system 192.168.34.56 is rebooting.
.............................................
..................................................
..........................................Done
........
..................................................
.....................
Status: Security erase for HDD is set for 192.168.34.56
WARNING: Without option --post_complete, please manually confirm the managed
system is POST complete before executing next action.
```

## Notes

- A Password/PSID file follows the CSV format with `;` (a semicolon) as the delimiter.
- `SecureEraseDisk` requires either the `--action` or `--precheck` option.
- By default, the NVMe vendor's driver is loaded by the BIOS to provide more information, but storage cannot be securely erased by the BIOS while it is loaded. Switch to the native AMI driver by changing the BIOS setting "NVMe Firmware Source" to "AMI Native Support," or if that setting is unavailable, set "Onboard NVMe Option ROM" to "Disabled."
- It is recommended that a password be assigned to the hard disk (an HDD without a password can be securely erased directly).
- An additional password cannot be assigned to an HDD that already has one installed, using SetPassword.
- Some BIOS may report Security Mode "NONE," equivalent to "Not TCG/SAT3 Supported."
- TCG supported devices can only be securely erased by `SecurityErasePSID`. SAT3 supported devices can only be securely erased by `SecurityErasePWD`, and the HDD password must be installed first. Some BIOS might not support security features for "Not TCG/SAT3 Supported" devices.
- Estimated secure erase time examples: 500GB SATA HDD is 98 minutes, 128GB SSD is 2 minutes, 512GB NVMe is a few seconds.
- Mismatched HDDs (no match between the serial number mapping file and the managed system) are recorded in a text file named `PreCheckFile`.
- Run pre-check mode before a secure erase. An HDD can only be securely erased after another erase task on it finishes.
- After the task completes, use the `GetCurrentBiosCfg` command and search for "Last Status Code" in the configuration file to check the result. A status code of zero indicates success; for non-zero codes, refer to Appendix D - Status Codes in UEFI Specification 2.8.
- For systems that do not support security erase automation, the erase procedure halts at a password prompt during system reboot.
