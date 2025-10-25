# UnmountIsoImage

Removes an ISO image as virtual media from the managed system.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> | [-I Redfish_HI]] [-u <username> -p <password>] -c UnmountIsoImage
```

### OpenBMC
```
sum -l <system list file> [-u <username> -p <password>] -c UnmountIsoImage
```

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UnmountIsoImage
```

### In-Band
```
[SUM_HOME]# ./sum -c UnmountIsoImage
```

### OpenBMC
```
[SUM_HOME]# ./sum -l SList.txt -u ADMIN -p PASSWORD -c UnmountIsoImage
```

## Notes

- Starting from SUM 2.11.0, this command is only supported on platforms that support a single virtual media device only.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/unmountisoimage.md