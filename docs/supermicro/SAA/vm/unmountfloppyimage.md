# UnmountFloppyImage

Virtually removes a binary floppy image from the managed system. This command is only supported on platforms that support a single virtual media device.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UnmountFloppyImage
```

### In-Band
```
saa -c UnmountFloppyImage
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UnmountFloppyImage
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UnmountFloppyImage
```

### In-Band
```bash
[SAA_HOME]# ./saa -c UnmountFloppyImage
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UnmountFloppyImage
```

## Output

```
SuperServer Automation Assistant 1.0.0 (2023/08/18) (x86_64)
Copyright(C) 2023 Super Micro Computer, Inc. All rights reserved.
Status: Checking node product key...
Status: The floppy image file is unmounting...
Status: The floppy image file is unmounted successfully.
```

If the execution "Status" field for a managed system is SUCCESS, the virtually mounted image will be removed from the managed system.

## Notes

- This command is only supported on platforms that support a single virtual media device only.
