# MountFloppyImage

Mounts a binary floppy image file to the managed system as virtual media. This command is only supported on platforms that support a single virtual media device.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c MountFloppyImage --file <filename>
```

### In-Band
```
saa -c MountFloppyImage --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c MountFloppyImage --file <filename>
```

## Options

- `--file <file name>`: Mounts the specified binary floppy file to the managed system.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountFloppyImage --file Floppy.img
```

### In-Band
```bash
[SAA_HOME]# ./saa -c MountFloppyImage --file Floppy.img
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c MountFloppyImage --file Floppy.img
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

```
SuperServer Automation Assistant 1.0.0 (2023/08/18) (x86_64)
Copyright(C) 2023 Super Micro Computer, Inc. All rights reserved.
Status: Checking node product key...
Status: The floppy image file "Floppy.img" is mounting...
.................
Status: The floppy image file "Floppy.img" is mounted successfully.
```

If the execution "Status" field of the managed system is SUCCESS, the floppy image is mounted virtually to the managed system.

## Notes

- This command is only supported on platforms that support a single virtual media device only.
- The floppy image size should be 1.44 MB.
