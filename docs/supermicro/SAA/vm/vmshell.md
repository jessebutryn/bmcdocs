# VMShell

Manages virtual media devices for the managed system from within SAA shell mode. This command is only available in SAA shell mode; enter shell mode first with `saa -i <IP or host name> -u <username> -p <password> -c Shell`.

## Syntax

### SAA Shell
```
VMShell --action <action> [--index <index>] [--file <file name>] [--dev_id <Device ID>]
```

## Actions

- **devlist**: Lists the available devices that can be mounted to virtual media device 1 of the BMC. Hard drives can be listed but cannot be mounted due to OS security concerns.
- **dev1drv**: Mounts a local USB device to virtual media device 1 of the BMC. Use `--index` to specify the index of the local USB device.
- **dev2iso**: Mounts a local ISO image file to virtual media device 2 of the BMC. Use `--file` to specify the local ISO image file.
- **dev1stop / dev2stop**: Stops virtual media device 1 or 2 of the BMC.
- **status**: Shows the status of virtual media devices of the BMC. Use `--dev_id` to specify a device; without it, status for all virtual media devices is listed.
- **log**: Shows the history of actions for the virtual media devices of the BMC.

## Options

- `--action <action>`: Sets action to 1 = devlist, 2 = dev1drv, 3 = dev1stop, 4 = dev2iso, 5 = dev2stop, 6 = status, 7 = log.
- `--file <file name>` (Optional): Mounts the ISO image file for virtual media device 2. Use it with the dev2iso action.
- `--dev_id <Device ID>` (Optional): Uses the specified device ID to get virtual media information. The supported device ID is [1-3]. Use it with the status action.
- `--index <index>` (Optional): Mounts the drive with the specified index for virtual media device 1. Use it with the dev1drv action.

## Examples

### devlist
```bash
[SAA_HOME]# X12_ATEN_AST2600> VMShell --action devlist
```

### dev1drv
```bash
[SAA_HOME]# X12_ATEN_AST2600> VMShell --action dev1drv --index 3
```

### dev2iso
```bash
[SAA_HOME]# X12_ATEN_AST2600> VMShell --action dev2iso --file efishell.iso
```

### dev1stop
```bash
[SAA_HOME]# X12_ATEN_AST2600> VMShell --action dev1stop
```

### log
```bash
[SAA_HOME]# X12_ATEN_AST2600> VMShell --action log
```

### status
```bash
[SAA_HOME]# X12_ATEN_AST2600> VMShell --action status
[SAA_HOME]# X12_ATEN_AST2600> VMShell --action status --dev_id 1
```

## Output

### devlist / dev1drv (multiple virtual media device platform)
```
......
3: [sdc1: SCSI Disk]
4: [sdd1: SCSI Disk]
5: [sda1: SCSI Disk]
6: [sdb1: SCSI Disk]
......
Mounting sdc1: SCSI Disk...
Device 1 : VM Plug-In OK!!
```

### dev2iso
```
......
Mounting ISO file: efishell.iso.............
Device 2 : VM Plug-In OK!!
```

### dev1stop
```
.........................
Device 1 : VM Plug-Out OK!! Stop!!
Device 1 : VM Plug-In OK!!
Device 2 : VM Plug-In OK!!
Device 1 : VM Plug-Out OK!! Stop!!
......
```

### status (multiple virtual media device platform)
```
Status: Start to get virtual media information.
Managed system................192.168.34.56
 Virtual media status......Enable
 Virtual media port........623
Virtual Media Device Information
=============================
 Device 1
 ============
 Device status: Mounted
 Media type: USBStick
 Connection setting: Applet
 Image: kvm_usb
 Device 2
 ============
 Device status: Mounted
 Media type: CD/DVD
 Connection setting: Applet
 Image: kvm_cd
 Device 3
 ============
 Device status: Unmounted
 Media type: N/A
 Connection setting: NotConnected
 Image: N/A
 SSL certificate verified: N/A
 Self-signed certificate accepted: N/A
 UserName: N/A
```

### status (single virtual media device platform)
```
Status: Start to get virtual media information.
Managed system................192.168.34.56
 Virtual media status......Enable
 Virtual media port........623
Virtual Media Device Information
=============================
 Device 1: Empty device
 Device 2: Disk Device
 Device 3: Empty device
```

## Notes

- Before running the `VMShell` command, you need to enter SAA shell mode (`saa ... -c Shell`).
- The maximum ISO image size is 10 GB.
- The floppy image size should be 1,474,560 bytes.
- Up to three virtual media devices are supported, including ISO and floppy images.
- If a device is mounted by iKVM, it can only be unmounted by iKVM.
