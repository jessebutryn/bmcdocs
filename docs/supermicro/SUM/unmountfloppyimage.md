# UnmountFloppyImage

Removes a binary floppy image virtually from the managed system.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c UnmountFloppyImage
```

### OpenBMC
```
sum -l <system list file> [-u <username> -p <password>] -c UnmountFloppyImage
```

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UnmountFloppyImage
```

### In-Band
```
[SUM_HOME]# ./sum -c UnmountFloppyImage
```

### OpenBMC
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c UnmountFloppyImage
```

## Notes

- Starting from SUM 2.11.0, this command is only supported on platforms that support single virtual media device only.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/unmountfloppyimage.md