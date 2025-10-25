# GetPMemInfo

## Description

Use the "GetPMemInfo" command to get the PMem firmware image information from the managed system as well as the local PMem firmware image (with the --file option).

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c GetPMemInfo [--file <filename> [--file_only]]
```

## Options

- `--file <filename>`: Specifies the local PMem firmware image file to read information from.
- `--file_only`: Reads information only from the local file specified by --file.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPMemInfo
The console output contains the following information.
Managed system................192.168.34.56
 PMem version..............2.2.0.1464
```

### In-Band
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c GetPMemInfo --file PMem.bin
The console output contains the following information.
Managed system................169.254.3.254
 PMem version..............2.2.0.1464
Local PMem image file.........PMem.bin
 PMem version..............2.2.0.1469
```

```
[SUM_HOME]# ./sum -c GetPMemInfo --file PMem.bin --file_only
The console output contains the following information.
Local PMem image file..........PMem.bin
 PMem version...............2.2.0.1469
```

## Notes

- This command is available on X12 3rd Gen Intel® Xeon® Scalable processors with Intel® C621A Series Chipsets and later platforms.
- The PMem firmware version retrieved from the "GetPMemInfo" command is the running PMem firmware version.
- For more detailed usages of PMem, please contact the technical support of Supermicro.
