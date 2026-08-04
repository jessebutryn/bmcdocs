# GetMotherboardFpgaInfo

Gets the motherboard FPGA firmware image and its corresponding information from the managed system. Can also read FPGA information from a local FPGA image file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetMotherboardFpgaInfo [--file <filename>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetMotherboardFpgaInfo [--file <filename>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetMotherboardFpgaInfo [--file <filename>]
```

## Options

- `--file <file name>` (Optional): Reads the motherboard FPGA information from an input FPGA image file.
- `--file_only` (Optional): Works with the `--file` option, and only reads motherboard FPGA information from the input image file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetMotherboardFpgaInfo --file FPGA.bin
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c GetMotherboardFpgaInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetMotherboardFpgaInfo
```

## Output

### Single System
```
Managed system..........................192.168.34.56
 Motherboard FPGA version............F3.74.23
Local FPGA image file...................FPGA.bin
 FPGA version........................F3.74.23
```

### Multiple Systems OOB
If the execution "Status" field for the managed system is SUCCESS, the FPGA information of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
