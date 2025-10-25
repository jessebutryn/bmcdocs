# GetMultinodeEcInfo

## Description

Use the "GetMultinodeEcInfo" command to get the multi-node EC firmware image information from the managed system as well as the local multi-node EC firmware image (with the --file option).

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c GetMultinodeEcInfo [--file <filename> [--file_only]]
```

## Options

- `--file <filename>`: Specifies the local EC firmware image file to read information from.
- `--file_only`: Reads information only from the local file specified by --file.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.184.11.65 -u ADMIN -p PASSWORD -c GetMultinodeEcInfo
The console output contains the following information.
Managed system............192.184.11.65
 EC ID.................A7
 EC version............1.20
```

### In-Band
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c GetMultinodeEcInfo
The console output contains the following information.
Managed system............169.254.3.254
 EC ID.................A7
 EC version............1.20
```

```
[SUM_HOME]# ./sum -c GetMultinodeEcInfo --file EC.bin --file_only
The console output contains the following information.
Local EC image file.......EC.bin
 EC ID.................A7
 EC version............1.20
```
