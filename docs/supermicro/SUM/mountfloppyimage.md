# MountFloppyImage

Mounts a binary floppy image as virtual media to the managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c MountFloppyImage --file <filename>
```

## Options

- `--file <filename>`: Path to the binary floppy image file to mount.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c MountFloppyImage --file Floppy.img
```

### In-Band
```
[SUM_HOME]# ./sum -c MountFloppyImage --file Floppy.img
```

## Notes

- Starting from SUM 2.11.0, this command is only supported on platforms that support a single virtual media device only.
- The floppy image size should be 1.44MB.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/mountfloppyimage.md