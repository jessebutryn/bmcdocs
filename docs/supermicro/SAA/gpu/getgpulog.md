# GetGpuLog

Saves the GPU dump log information of the managed system to a file, for HGX and AMD MI300X systems. Also supports downloading the HGX Debug Token certificate log.

## Syntax

### Single System

#### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetGpuLog --item <item name> --file <file name> [--overwrite]
```

#### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetGpuLog --item <item name> --file <file name> [--overwrite]
```

### Multiple Systems

#### OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetGpuLog --item <item name> --file <file name> [--overwrite]
```

## Options

- `--file <file name>`: Saves the GPU log to a file.
- `--item <item name>`: Item type of GPU. Values: `1 = HGX`, `2 = MI300X`.
- `--type <type>`: `1 = DebugToken`. Only used for downloading the Debug Token certificate log file.
- `--overwrite`: Overwrites the output file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetGpuLog --item HGX --file log.tgz

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetGpuLog --item HGX --type DebugToken --file DebugToken.log

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetGpuLog --item MI300X --file log.tgz
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetGpuLog --item HGX --file log.tgz

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetGpuLog --item HGX --type DebugToken --file DebugToken.log

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetGpuLog --item MI300X --file log.tgz
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetGpuLog --item HGX --file log.tgz
```

## Output

### HGX / MI300X Log
```
Creating the GPU Log file ...
..................................................
..................................................
The GPU Log download file is ready.
File "log.tgz" is created.
```

### HGX Debug Token Certificate
```
Creating the GPU Debug Token Log file ...
Downloading the GPU Debug Token Log file ...
.......
The GPU Log download file is ready.
File "DebugToken.log" is created.
```

## Notes

- If the "Status" field in the execution of the managed system shows SUCCESS, the console output of the managed system will be displayed in the "Execution Message" section of the log file created for the managed system.
