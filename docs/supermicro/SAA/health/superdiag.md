# SuperDiag

Runs BIOS diagnostic functions remotely using Super Diagnostics Offline (SDO), a system diagnostic tool that runs in the EFI shell to determine the health of a Supermicro server's components. Supported actions are Start, Download, Display, and List, and diagnostics can also run in embedded mode.

## Getting the SuperDiag ISO Image

1. Download the zip file `SuperDiag_x.x.x_Tyyyymmdd.zip` from the Supermicro download center.
2. Unzip it to create a folder named `SuperDiag_x.x.x_Tyyyymmdd`.
3. Locate `ISOForSuperDiag.zip` within the `SuperDiag_x.x.x_Tyyyymmdd\Diagnose_Remotely` subfolder to get the ISO image `SuperDiag.x.x.x.iso`.

## Creating a SuperDiag Pen Drive

1. Download the zip file `SuperDiag_x.x.x_Tyyyymmdd.zip` from the Supermicro download center.
2. Unzip it to create a folder named `SuperDiag_x.x.x_Tyyyymmdd`.
3. Locate `USBForSuperDiag.zip` within the `SuperDiag_x.x.x_Tyyyymmdd\Diagnose_Remotely` subfolder, unzip it, and copy the extracted contents to a pen drive.

## Syntax

### Start (OOB)
```
saa -i <IP or host name> -u <username> -p <password> -c SuperDiag --action Start {--file <ISO image> | --image_url <URL of ISO image> [--dev_id <index>] | --usb --index <index>} --reboot
```

### Start (Multiple Systems OOB)
```
saa -l <system list file> -c SuperDiag --action Start --file --image_url <URL of ISO image> [--dev_id <index>] --reboot
```

### Start Embedded Mode (OOB)
```
saa -i <IP or host name> -u <username> -p <password> -c SuperDiag --action Start --embedded --reboot
```

### Start Embedded Mode (Multiple Systems OOB)
```
saa -l <system list file> -c SuperDiag --action Start --embedded --reboot
```

### Download (OOB / In-Band)
```
saa -i <IP or host name> -u <username> -p <password> -c SuperDiag --action Download --file <results.json> [--overwrite]
saa -c SuperDiag --action Download --file <results.json> [--overwrite]
```

### Download (Multiple Systems OOB)
```
saa -l <system list file> -c SuperDiag --action Download --file <results.json> [--overwrite]
```

### Download Embedded Mode (OOB / In-Band)
```
saa -i <IP or host name> -u <username> -p <password> -c SuperDiag --action Download --embedded --file <results.html> [--overwrite]
saa -c SuperDiag --action Download --embedded --file <results.html> [--overwrite]
```

### Download Embedded Mode (Multiple Systems OOB)
```
saa -l <system list file> -c SuperDiag --action Download --file <results.html> [--overwrite]
```

### Display (In-Band)
```
saa -c SuperDiag --action Display --file <results.json> [--type <display type>] [--keyword <keyword>] [--line <number>]
```

### List (OOB / In-Band)
```
saa -i <IP or host name> -u <username> -p <password> -c SuperDiag --action List --usb
saa -c SuperDiag --action List --usb
```

## Options

- `--action <action>`: Sets SuperDiag action:
    - `1` = Start
    - `2` = Download
    - `3` = Display
    - `4` = List
- `--file <file name>`: (Optional) For Start: mounts the ISO image to run diagnostics. For Download/Display: the filename for diagnostic results.
- `--image_url <URL>`: (Optional) The URL to access the shared ISO image file, in the format `http://<IPv4 or IPv6>/<shared point>/<file path>` or `https://<IPv4 or IPv6>/<shared point>/<file path>`.
- `--dev_id <Device ID>`: (Optional) The specified device to mount the ISO image. Supported device IDs: 1-3.
- `--overwrite`: (Optional) Overwrites the diagnostic results file.
- `--reboot`: (Optional) Forces the managed system to reboot or power up after the operation.
- `--type <type>`: (Optional) Sets display type: `0` = Info, `1` = Pass, `2` = Fail. The input type string is converted to the above type number.
- `--line <number>`: (Optional) Prints the given number of lines at a time.
- `--usb`: (Optional) For action Start: starts a diagnostic with a local USB device. For action List: lists available device indexes to mount local USB.
- `--index <index>`: (Optional) The specified index to mount local USB.

## Examples

### Starting Diagnostics (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SuperDiag --action Start --file SuperDiag_1.9.0.iso --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SuperDiag --action Start --image_url '\2001:db8::1\MySharedPoint\MyFolder\Image.iso' --dev_id 2 --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SuperDiag --action Start --usb --index 3 --reboot
```

### Downloading Diagnostic Results (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SuperDiag --action Download --file results.json
```

### Downloading Diagnostic Results (In-Band)
```bash
[SAA_HOME]# ./saa -c SuperDiag --action Download --file results.json
```

### Displaying Diagnostic Results (In-Band)
```bash
[SAA_HOME]# ./saa -c SuperDiag --action Display --file results.json --type info --keyword BIOS

[SAA_HOME]# ./saa -c SuperDiag --action Display --file results.json --type fail --line 20
```

### Listing Available Devices (In-Band)
```bash
[SAA_HOME]# ./saa -c SuperDiag --action List --usb
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SuperDiag --action Start --image_url '\2001:db8::1\MySharedPoint\MyFolder\Image.iso' --dev_id 2 --reboot

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SuperDiag --action Download --file results.json
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system is shown in the "Execution Message" section of the created log file.

## Output

### Display (--type fail example)
```
System Component Detection:
 RAID Detection:
 Device presence check:
 Result: Aborted
 Backplane Detection:
 Device presence check:
 Result: Aborted
 GPU Detection:
 Device presence check:
 Result: Aborted
CPU Diagnostics:
 CPU #001 - AMD Eng Sample: 100-000000897-03 :
 Brand-string Test:
 Result: Failed
Network Diagnostics:
 Broadcom Ethernet BCM57416/5720L #2:
 Network Connection:
 Result: Aborted
PCIe Diagnostics:
 ASPEED Video AST2600:
```

### List --usb
```
....
3: [sdc1: SCSI Disk]
4: [sda1: SCSI Disk]
5: [sdb1: SCSI Disk]
```

## Notes

- `--action Start` does not support In-Band usage.
- `--action Display` does not support OOB usage or multiple-systems OOB usage.
- `--action List` can display available hard drives, but they cannot be used with `--action Start` for diagnostics due to security restrictions.
- In embedded mode, downloaded diagnostic results are in HTML format; open the HTML file in a browser to check the results.
