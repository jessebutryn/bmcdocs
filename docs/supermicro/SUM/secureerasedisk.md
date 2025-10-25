# SecureEraseDisk

Securely erases hard disks on the managed system using various security modes and methods.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c SecureEraseDisk [[--current_password <current password>] | [--cur_pw_file <current password file path>]] --file <filename> [[--action <action> --reboot] | [--precheck]]
```

## Options

- `--current_password <current password>`: Current password for authentication.
- `--cur_pw_file <current password file path>`: File containing the current password.
- `--file <filename>`: Input file containing disk information (PSID.txt or Password.txt).
- `--action <action>`: Action to perform (see Actions section).
- `--reboot`: Forces the managed system to reboot after the operation.
- `--precheck`: Performs pre-check to show disk information and supported actions.

## Actions

### TCG Supported Devices
- `SetPassword`: Sets an HDD password.
- `ChangePassword`: Changes the HDD password.
- `ClearPassword`: Clears the HDD password.
- `SecurityErase`: Erases a device without an HDD password installed.
- `SecurityErasePWD`: Erases a device with an HDD password.
- `SecurityErasePSID`: Erases a device with PSID.

### SAT3 Supported Devices
- `SetPassword`: Sets an HDD password.
- `ChangePassword`: Changes the HDD password.
- `ClearPassword`: Clears the HDD password.
- `SecurityErase`: Erases a device without an HDD password installed.
- `SecurityErasePWD`: Erases a device with an HDD password.
- `SecurityErasePSID`: Erases a device with PSID.

### Not TCG/SAT3 Supported Devices
- `SecurityErase`: Erases a device without an HDD password installed.

## Input File Formats

### PSID.txt
Format: `serial number;PSID`
```
W472TJXH;HR1MJDCKLH4CD88ELEGDUE5J4UA3QGZZ
```

### Password.txt
Format: `serial number;password;new_password` (new_password required for ChangePassword, optional for others)
```
9XF4AF7M;123456;111111
W472TJXH;123456;111111
```

## Execution Modes

### Action Mode
Performs secure erase operations. Requires system reboot for changes to take effect.

### Pre-check Mode
Shows information about HDDs:
- Password Status: Whether a password is installed
- Security Mode: TCG, SAT3, or Not TCG/SAT3 Supported
- TCG Device Type: Device type for TCG supported HDDs
- Applicable Actions: Actions that can be executed on the HDD
- Estimated Execution Time: Time required for secure erase
- No Matched HDDs: HDDs that couldn't be matched (saved to PreCheckFile)

## Examples

### Pre-check with PSID file (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseDisk --file PSID.txt --precheck
```

### Pre-check with Password file (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseDisk --file Password.txt --precheck
```

### Set Password (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseDisk --file Password.txt --action SetPassword --reboot
```

### Security Erase (OOB)
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SecureEraseDisk --file Password.txt --action SecurityErase --reboot
```

### Security Erase with PSID (In-Band)
```
[SUM_HOME]# ./sum -c SecureEraseDisk --file PSID.txt --action SecurityErasePSID --reboot
```

### Security Erase with Password (In-Band)
```
[SUM_HOME]# ./sum -c SecureEraseDisk --file Password.txt --action SecurityErasePWD --reboot
```

## Notes

- The SecureEraseDisk command requires either the --action or --precheck option.
- By default, the NVMe vendor's driver will be loaded by BIOS, but when loaded, storage cannot be securely erased by BIOS. Switch to the native AMI driver by changing BIOS setting "NVMe Firmware Source" to "AMI Native Support", or "Onboard NVMe Option ROM" to "Disabled".
- An HDD without a password installed can be securely erased without a password or PSID, so it is recommended that a password be assigned to the hard disk.
- Another password cannot be assigned to an HDD with a password already installed by SetPassword action.
- Some BIOS may be in Security Mode "NONE", which is the same as "Not TCG/SAT3 Supported".
- BIOS limitations:
  - TCG supported devices can only be securely erased by "SecurityErasePSID"
  - SAT3 supported devices can only be securely erased by "SecurityErasePWD", and the HDD password must be installed before erasing
  - Some BIOS might not support security features for "Not TCG/SAT3 Supported" devices
- Estimated erase times:
  - 500GB SATA HDD: 98 minutes
  - 128GB SSD: 2 minutes
  - 512GB NVMe: a few seconds
- Supported platforms:
  - X11 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series Chipsets
  - X11 8th/9th Generation Intel® Core™ i3/Pentium®/Celeron® Processor, X11 Intel® Xeon® E-2100 Processor and X11 Intel® Xeon® E-2200 Processor with Intel® C622 Controller
  - X12 Intel® Xeon® Scalable Processors with Intel® C620 Series Chipsets
  - X12 12th Generation Intel® Core™ Processors with Intel® B660/Z690/H610 Chipsets
- After completion, use GetCurrentBiosCfg to check the result by looking for "Last Status Code" in the configuration file. A status code of zero indicates success.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/secureerasedisk.md